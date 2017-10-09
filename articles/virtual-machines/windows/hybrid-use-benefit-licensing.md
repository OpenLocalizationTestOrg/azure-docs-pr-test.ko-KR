---
title: "Windows Server 및 Windows 클라이언트에 대 한 하이브리드 사용 혜택 aaaAzure | Microsoft Docs"
description: "어떻게 toomaximize Windows Software Assurance 혜택 toobring 온-프레미스에 알아봅니다 tooAzure 라이선스"
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
ms.openlocfilehash: f24487320a60132aaf766a31f3e6f3726d4a3bd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-hybrid-use-benefit-for-windows-server-and-windows-client"></a><span data-ttu-id="f8d2c-103">Window Server 및 Windows 클라이언트에 대한 Azure 하이브리드 사용 혜택</span><span class="sxs-lookup"><span data-stu-id="f8d2c-103">Azure Hybrid Use Benefit for Windows Server and Windows Client</span></span>
<span data-ttu-id="f8d2c-104">Software Assurance와 함께 고객에 대 한 Azure 하이브리드 사용 혜택 사용 하면 toouse 온-프레미스 Windows Server 및 Windows 클라이언트 라이선스 및 저렴된 한 비용에 Azure에서 실행된 Windows 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="f8d2c-104">For customers with Software Assurance, Azure Hybrid Use Benefit allows you toouse your on-premises Windows Server and Windows Client licenses and run Windows virtual machines in Azure at a reduced cost.</span></span> <span data-ttu-id="f8d2c-105">Windows Server에 대한 Azure 하이브리드 사용 혜택에는 Windows Server 2008R2, Windows Server 2012, Windows Server 2012R2 및 Windows Server 2016이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8d2c-105">Azure Hybrid Use Benefit for Windows Server includes Windows Server 2008R2, Windows Server 2012, Windows Server 2012R2, and Windows Server 2016.</span></span> <span data-ttu-id="f8d2c-106">Windows 클라이언트에 대한 Azure 하이브리드 사용 혜택에는 Windows 10이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8d2c-106">Azure Hybrid Use Benefit for Windows Client includes Windows 10.</span></span> <span data-ttu-id="f8d2c-107">자세한 내용은 hello를 참조 하십시오 [Azure 하이브리드 사용 혜택 라이선스 페이지](https://azure.microsoft.com/pricing/hybrid-use-benefit/)합니다.</span><span class="sxs-lookup"><span data-stu-id="f8d2c-107">For more information, please see hello [Azure Hybrid Use Benefit licensing page](https://azure.microsoft.com/pricing/hybrid-use-benefit/).</span></span>

>[!IMPORTANT]
><span data-ttu-id="f8d2c-108">Azure 하이브리드 사용 이점에 대 한 Windows 클라이언트는 현재 미리 보기로 hello Windows 10 이미지를 사용 하 여 hello Azure Marketplace에서.</span><span class="sxs-lookup"><span data-stu-id="f8d2c-108">Azure Hybrid Use Benefits for Windows Client is currently in Preview using hello Windows 10 image in hello Azure Marketplace.</span></span> <span data-ttu-id="f8d2c-109">사용자별 Windows 10 Enterprise E3/E5 또는 사용자별 Windows VDA(사용자 구독 라이선스 또는 추가 기능 사용자 구독 라이선스)를 보유한 엔터프라이즈 고객("적격 라이선스")만 혜택을 누릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8d2c-109">Only Enterprise customers with Windows 10 Enterprise E3/E5 per user or Windows VDA per user (User Subscription Licenses or Add-on User Subscription Licenses) (“Qualifying Licenses”) are eligible.</span></span>
>
>

## <a name="ways-toouse-azure-hybrid-use-benefit"></a><span data-ttu-id="f8d2c-110">같은 방법으로 toouse Azure 하이브리드 사용 이점</span><span class="sxs-lookup"><span data-stu-id="f8d2c-110">Ways toouse Azure Hybrid Use Benefit</span></span>
<span data-ttu-id="f8d2c-111">Azure 하이브리드 사용 혜택 hello로 다양 한 방법 toodeploy Windows Vm의 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8d2c-111">There are a couple of different ways toodeploy Windows VMs with hello Azure Hybrid Use Benefit:</span></span>

1. <span data-ttu-id="f8d2c-112">Azure 하이브리드 사용 혜택을 이용하여 미리 구성된 [특정 Marketplace 이미지](#deploy-a-vm-using-the-azure-marketplace)(Windows Server 2016, Windows Server 2012R2, Windows Server 2012 및 Windows Server 2008SP1)에서 VM을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8d2c-112">You can deploy VMs from [specific Marketplace images](#deploy-a-vm-using-the-azure-marketplace) that are pre-configured with Azure Hybrid Use Benefit - Windows Server 2016, Windows Server 2012R2, Windows Server 2012 and Windows Server 2008SP1.</span></span>
2. <span data-ttu-id="f8d2c-113">[사용자 지정 VM을 업로드](#upload-a-windows-vhd)하거나 [Resource Manager 템플릿](#deploy-a-vm-via-resource-manager) 또는 [Azure PowerShell을 사용하여 배포](#detailed-powershell-deployment-walkthrough)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8d2c-113">You can [upload a custom VM](#upload-a-windows-vhd) and [deploy using a Resource Manager template](#deploy-a-vm-via-resource-manager) or [Azure PowerShell](#detailed-powershell-deployment-walkthrough).</span></span>

## <a name="deploy-a-vm-using-hello-azure-marketplace"></a><span data-ttu-id="f8d2c-114">Hello Azure Marketplace를 사용 하 여 VM 배포</span><span class="sxs-lookup"><span data-stu-id="f8d2c-114">Deploy a VM using hello Azure Marketplace</span></span>
<span data-ttu-id="f8d2c-115">다음 이미지는 hello Azure 하이브리드 사용 혜택으로 미리 구성 하는 Marketplace에서에서 사용할 수 있습니다.: Windows Server 2016, Windows Server 2012 r 2, Windows Server 2012 및 Windows Server 2008SP1 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8d2c-115">Following images are available in hello Marketplace pre-configured with Azure Hybrid Use Benefit: Windows Server 2016, Windows Server 2012R2, Windows Server 2012 and Windows Server 2008SP1.</span></span> <span data-ttu-id="f8d2c-116">이러한 이미지는 Azure 포털 hello, 리소스 관리자 템플릿 또는 Azure PowerShell에서 직접 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8d2c-116">These images can be deployed directly from hello Azure portal, Resource Manager templates, or Azure PowerShell.</span></span>

<span data-ttu-id="f8d2c-117">Hello Azure 포털에서 직접 이러한 이미지를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8d2c-117">You can deploy these images directly from hello Azure portal.</span></span> <span data-ttu-id="f8d2c-118">리소스 관리자 템플릿을 Azure PowerShell을 사용 하 여 사용 하기 위해 볼 hello 이미지 목록이 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f8d2c-118">For use in Resource Manager templates and with Azure PowerShell, view hello list of images as follows:</span></span>

<span data-ttu-id="f8d2c-119">Windows Server:</span><span class="sxs-lookup"><span data-stu-id="f8d2c-119">For Windows Server:</span></span>
```powershell
Get-AzureRmVMImagesku -Location westus -PublisherName MicrosoftWindowsServer -Offer WindowsServer
```
- <span data-ttu-id="f8d2c-120">2016-Datacenter 버전 2016.127.20170406 이상</span><span class="sxs-lookup"><span data-stu-id="f8d2c-120">2016-Datacenter version 2016.127.20170406 or above</span></span>

- <span data-ttu-id="f8d2c-121">2012-R2-Datacenter 버전 4.127.20170406 이상</span><span class="sxs-lookup"><span data-stu-id="f8d2c-121">2012-R2-Datacenter version 4.127.20170406 or above</span></span>

- <span data-ttu-id="f8d2c-122">2012-Datacenter 버전 3.127.20170406 이상</span><span class="sxs-lookup"><span data-stu-id="f8d2c-122">2012-Datacenter version 3.127.20170406 or above</span></span>

- <span data-ttu-id="f8d2c-123">2008-R2-SP1 버전 2.127.20170406 이상</span><span class="sxs-lookup"><span data-stu-id="f8d2c-123">2008-R2-SP1 version 2.127.20170406 or above</span></span>

<span data-ttu-id="f8d2c-124">Windows 클라이언트:</span><span class="sxs-lookup"><span data-stu-id="f8d2c-124">For Windows Client:</span></span>
```powershell
Get-AzureRMVMImageSku -Location "West US" -Publisher "MicrosoftWindowsServer" `
    -Offer "Windows-HUB"
```

## <a name="upload-a-windows-server-vhd"></a><span data-ttu-id="f8d2c-125">Windows Server VHD 업로드</span><span class="sxs-lookup"><span data-stu-id="f8d2c-125">Upload a Windows Server VHD</span></span>
<span data-ttu-id="f8d2c-126">Azure에서 Windows Server VM toodeploy 먼저 toocreate 기본 Windows 빌드를 포함 하는 VHD입니다.</span><span class="sxs-lookup"><span data-stu-id="f8d2c-126">toodeploy a Windows Server VM in Azure, you first need toocreate a VHD that contains your base Windows build.</span></span> <span data-ttu-id="f8d2c-127">TooAzure 업로드 하기 전에이 VHD Sysprep을 통해 적절 하 게 준비 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8d2c-127">This VHD must be appropriately prepared via Sysprep before you upload it tooAzure.</span></span> <span data-ttu-id="f8d2c-128">있습니다 수 [hello VHD 요구 사항 및 Sysprep 프로세스에 대 한 자세한](upload-generalized-managed.md) 및 [서버 역할에 대 한 Sysprep 지원](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)합니다.</span><span class="sxs-lookup"><span data-stu-id="f8d2c-128">You can [read more about hello VHD requirements and Sysprep process](upload-generalized-managed.md) and [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span></span> <span data-ttu-id="f8d2c-129">Sysprep를 실행 하기 전에 hello VM 백업 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8d2c-129">Back up hello VM before running Sysprep.</span></span> 

<span data-ttu-id="f8d2c-130">있는지 [최신 Azure PowerShell 설치 및 구성 된 hello](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="f8d2c-130">Make sure you have [installed and configured hello latest Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="f8d2c-131">VHD를 준비 했으면, 업로드 hello를 사용 하 여 hello VHD tooyour Azure 저장소 계정을 `Add-AzureRmVhd` 다음과 같이 cmdlet:</span><span class="sxs-lookup"><span data-stu-id="f8d2c-131">Once you have prepared your VHD, upload hello VHD tooyour Azure Storage account using hello `Add-AzureRmVhd` cmdlet as follows:</span></span>

```powershell
Add-AzureRmVhd -ResourceGroupName "myResourceGroup" -LocalFilePath "C:\Path\To\myvhd.vhd" `
    -Destination "https://mystorageaccount.blob.core.windows.net/vhds/myvhd.vhd"
```

> [!NOTE]
> <span data-ttu-id="f8d2c-132">Microsoft SQL Server, SharePoint 서버 및 Dynamics는 또한 Software Assurance 라이선스를 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8d2c-132">Microsoft SQL Server, SharePoint Server, and Dynamics can also utilize your Software Assurance licensing.</span></span> <span data-ttu-id="f8d2c-133">응용 프로그램 구성 요소를 설치 하 고 라이선스 키를 적절 하 게 제공 다음 hello 디스크 이미지 tooAzure 업로드 하 여 tooprepare hello Windows Server 이미지를 여전히 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8d2c-133">You still need tooprepare hello Windows Server image by installing your application components and providing license keys accordingly, then uploading hello disk image tooAzure.</span></span> <span data-ttu-id="f8d2c-134">Hello와 같은 응용 프로그램에 Sysprep를 실행 하기 위한 적절 한 설명서를 검토 [Sysprep를 사용 하 여 SQL Server 설치를 위한 고려 사항](https://msdn.microsoft.com/library/ee210754.aspx) 또는 [(Sysprep)SharePointServer2016참조이미지만들기](http://social.technet.microsoft.com/wiki/contents/articles/33789.build-a-sharepoint-server-2016-reference-image-sysprep.aspx).</span><span class="sxs-lookup"><span data-stu-id="f8d2c-134">Review hello appropriate documentation for running Sysprep with your application, such as [Considerations for Installing SQL Server using Sysprep](https://msdn.microsoft.com/library/ee210754.aspx) or [Build a SharePoint Server 2016 Reference Image (Sysprep)](http://social.technet.microsoft.com/wiki/contents/articles/33789.build-a-sharepoint-server-2016-reference-image-sysprep.aspx).</span></span>
>
>

<span data-ttu-id="f8d2c-135">또한 자세한 방법에 대 한 [hello VHD tooAzure 프로세스를 업로드 하는 중](upload-generalized-managed.md#upload-the-vhd-to-your-storage-account)</span><span class="sxs-lookup"><span data-stu-id="f8d2c-135">You can also read more about [uploading hello VHD tooAzure process](upload-generalized-managed.md#upload-the-vhd-to-your-storage-account)</span></span>


## <a name="deploy-a-vm-via-resource-manager-template"></a><span data-ttu-id="f8d2c-136">Resource Manager 템플릿을 통해 VM 배포</span><span class="sxs-lookup"><span data-stu-id="f8d2c-136">Deploy a VM via Resource Manager Template</span></span>
<span data-ttu-id="f8d2c-137">Resource Manager 템플릿 내에서 `licenseType` 에 대한 추가 매개 변수를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8d2c-137">Within your Resource Manager templates, an additional parameter for `licenseType` can be specified.</span></span> <span data-ttu-id="f8d2c-138">[Azure Resource Manager 템플릿 작성](../../resource-group-authoring-templates.md)에 대해 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8d2c-138">You can read more about [authoring Azure Resource Manager templates](../../resource-group-authoring-templates.md).</span></span> <span data-ttu-id="f8d2c-139">VHD 업로드 tooAzure를 만든 후 편집 하면 리소스 관리자 템플릿 tooinclude hello 라이선스 유형 hello의 일부 공급자를 계산 하 고 일반적인 방법으로 템플릿을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8d2c-139">Once you have your VHD uploaded tooAzure, edit you Resource Manager template tooinclude hello license type as part of hello compute provider and deploy your template as normal:</span></span>

<span data-ttu-id="f8d2c-140">Windows Server:</span><span class="sxs-lookup"><span data-stu-id="f8d2c-140">For Windows Server:</span></span>
```json
"properties": {  
   "licenseType": "Windows_Server",
   "hardwareProfile": {
        "vmSize": "[variables('vmSize')]"
   }
```

<span data-ttu-id="f8d2c-141">Windows 클라이언트 toouse Azure 마켓플레이스 이미지와만에 대 한:</span><span class="sxs-lookup"><span data-stu-id="f8d2c-141">For Windows Client toouse with Azure Marketplace Image only:</span></span>
```json
"properties": {  
   "licenseType": "Windows_Client",
   "hardwareProfile": {
        "vmSize": "[variables('vmSize')]"
   }
```

## <a name="deploy-a-vm-via-powershell-quickstart"></a><span data-ttu-id="f8d2c-142">PowerShell 빠른 시작을 통해 VM 배포</span><span class="sxs-lookup"><span data-stu-id="f8d2c-142">Deploy a VM via PowerShell quickstart</span></span>
<span data-ttu-id="f8d2c-143">PowerShell을 통해 Windows Server VM을 배포할 때는 `-LicenseType`에 대한 추가 매개 변수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8d2c-143">When deploying your Windows Server VM via PowerShell, you have an additional parameter for `-LicenseType`.</span></span> <span data-ttu-id="f8d2c-144">사용 하 여 VM을 만들 VHD 업로드 tooAzure를 만든 후 `New-AzureRmVM` hello 라이선스 유형을 다음과 같이 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8d2c-144">Once you have your VHD uploaded tooAzure, you create a VM using `New-AzureRmVM` and specify hello licensing type as follows:</span></span>

<span data-ttu-id="f8d2c-145">Windows Server:</span><span class="sxs-lookup"><span data-stu-id="f8d2c-145">For Windows Server:</span></span>
```powershell
New-AzureRmVM -ResourceGroupName "myResourceGroup" -Location "West US" -VM $vm -LicenseType "Windows_Server"
```

<span data-ttu-id="f8d2c-146">Windows 클라이언트 toouse Azure 마켓플레이스 이미지와만에 대 한:</span><span class="sxs-lookup"><span data-stu-id="f8d2c-146">For Windows Client toouse with Azure Marketplace Image only:</span></span>
```powershell
New-AzureRmVM -ResourceGroupName "myResourceGroup" -Location "West US" -VM $vm -LicenseType "Windows_Client"
```

<span data-ttu-id="f8d2c-147">할 수 있습니다 [PowerShell 통해 Azure에서 VM 배포에 보다 자세한 연습 읽을](hybrid-use-benefit-licensing.md#detailed-powershell-deployment-walkthrough) 에 보다 설명적인 가이드 hello 너무 다른 단계가 아래 또는 읽기[리소스 관리자 및 PowerShell를사용하여WindowsVM을만들](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f8d2c-147">You can [read a more detailed walkthrough on deploying a VM in Azure via PowerShell](hybrid-use-benefit-licensing.md#detailed-powershell-deployment-walkthrough) below, or read a more descriptive guide on hello different steps too[create a Windows VM using Resource Manager and PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


## <a name="verify-your-vm-is-utilizing-hello-licensing-benefit"></a><span data-ttu-id="f8d2c-148">VM hello 라이선스 혜택을 활용 하는 확인</span><span class="sxs-lookup"><span data-stu-id="f8d2c-148">Verify your VM is utilizing hello licensing benefit</span></span>
<span data-ttu-id="f8d2c-149">Hello PowerShell 또는 리소스 관리자 배포 방법 중 하나를 통해 VM을 배포한 후 확인 된 hello 라이선스 유형을 `Get-AzureRmVM` 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f8d2c-149">Once you have deployed your VM through either hello PowerShell or Resource Manager deployment method, verify hello license type with `Get-AzureRmVM` as follows:</span></span>

```powershell
Get-AzureRmVM -ResourceGroup "myResourceGroup" -Name "myVM"
```

<span data-ttu-id="f8d2c-150">hello는 비슷한 toohello 다음 예제에서는 Windows Server에 대 한 출력:</span><span class="sxs-lookup"><span data-stu-id="f8d2c-150">hello output is similar toohello following example for Windows Server:</span></span>

```powershell
Type                     : Microsoft.Compute/virtualMachines
Location                 : westus
LicenseType              : Windows_Server
```

<span data-ttu-id="f8d2c-151">이 출력 다음 VM hello Azure 갤러리에서 직접 배포 된 VM과 같은 Azure 하이브리드 사용 혜택 라이선스 없이 배포 된 hello와 대조 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8d2c-151">This output contrasts with hello following VM deployed without Azure Hybrid Use Benefit licensing, such as a VM deployed straight from hello Azure Gallery:</span></span>

```powershell
Type                     : Microsoft.Compute/virtualMachines
Location                 : westus
LicenseType              :
```

## <a name="detailed-powershell-deployment-walkthrough"></a><span data-ttu-id="f8d2c-152">자세한 PowerShell 배포 연습</span><span class="sxs-lookup"><span data-stu-id="f8d2c-152">Detailed PowerShell deployment walkthrough</span></span>
<span data-ttu-id="f8d2c-153">hello 다음 PowerShell 단계 표시 VM의 전체 배포를 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f8d2c-153">hello following detailed PowerShell steps show a full deployment of a VM.</span></span> <span data-ttu-id="f8d2c-154">Toohello 실제 cmdlet에서 생성 되 고 다른 구성 요소와 더 많은 컨텍스트를 읽을 수 [리소스 관리자 및 PowerShell을 사용 하 여 Windows VM을 만들](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="f8d2c-154">You can read more context as toohello actual cmdlets and different components being created in [Create a Windows VM using Resource Manager and PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="f8d2c-155">단계별로 리소스 그룹, 저장소 계정 및 가상 네트워킹을 만든 다음 VM을 정의하고 마지막으로 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f8d2c-155">You step through creating your resource group, storage account, and virtual networking, then define your VM and finally create your VM.</span></span>

<span data-ttu-id="f8d2c-156">먼저 안전하게 자격 증명을 얻고, 위치를 설정하고, 리소스 그룹 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f8d2c-156">First, securely obtain credentials, set a location, and resource group name:</span></span>

```powershell
$cred = Get-Credential
$location = "West US"
$resourceGroupName = "myResourceGroup"
```

<span data-ttu-id="f8d2c-157">공용 IP 만들기:</span><span class="sxs-lookup"><span data-stu-id="f8d2c-157">Create a public IP:</span></span>

```powershell
$publicIPName = "myPublicIP"
$publicIP = New-AzureRmPublicIpAddress -Name $publicIPName -ResourceGroupName $resourceGroupName `
    -Location $location -AllocationMethod "Dynamic"
```

<span data-ttu-id="f8d2c-158">서브넷, NIC 및 VNET을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="f8d2c-158">Define your subnet, NIC, and VNET:</span></span>

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

<span data-ttu-id="f8d2c-159">VM 이름을 지정하고 VM 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f8d2c-159">Name your VM and create a VM config:</span></span>

```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A1"
```

<span data-ttu-id="f8d2c-160">OS 정의:</span><span class="sxs-lookup"><span data-stu-id="f8d2c-160">Define your OS:</span></span>

```powershell
$computerName = "myVM"
$vm = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $computerName -Credential $cred `
    -ProvisionVMAgent -EnableAutoUpdate
```

<span data-ttu-id="f8d2c-161">프로그램 NIC toohello VM을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8d2c-161">Add your NIC toohello VM:</span></span>

```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

<span data-ttu-id="f8d2c-162">저장소 계정 toouse hello를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8d2c-162">Define hello storage account toouse:</span></span>

```powershell
$storageAcc = Get-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -AccountName mystorageaccount
```

<span data-ttu-id="f8d2c-163">적절 하 게 준비 된 VHD를 업로드 하 고 사용 하기 위해 VM tooyour 연결:</span><span class="sxs-lookup"><span data-stu-id="f8d2c-163">Upload your VHD, suitably prepared, and attach tooyour VM for use:</span></span>

```powershell
$osDiskName = "licensing.vhd"
$osDiskUri = '{0}vhds/{1}{2}.vhd' -f $storageAcc.PrimaryEndpoints.Blob.ToString(), $vmName.ToLower(), $osDiskName
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/vhd/myvhd.vhd"
$vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri -CreateOption FromImage `
    -SourceImageUri $urlOfUploadedImageVhd -Windows
```

<span data-ttu-id="f8d2c-164">마지막으로, VM 만들고 형식 tooutilize Azure 하이브리드 사용 혜택 라이선스 hello 정의:</span><span class="sxs-lookup"><span data-stu-id="f8d2c-164">Finally, create your VM and define hello licensing type tooutilize Azure Hybrid Use Benefit:</span></span>

<span data-ttu-id="f8d2c-165">Windows Server:</span><span class="sxs-lookup"><span data-stu-id="f8d2c-165">For Windows Server:</span></span>
```powershell
New-AzureRmVM -ResourceGroupName $resourceGroupName -Location $location -VM $vm -LicenseType "Windows_Server"
```

## <a name="deploy-a-virtual-machine-scale-set-via-resource-manager-template"></a><span data-ttu-id="f8d2c-166">Resource Manager 템플릿을 사용하여 가상 컴퓨터 크기 집합 배포</span><span class="sxs-lookup"><span data-stu-id="f8d2c-166">Deploy a virtual machine scale set via Resource Manager template</span></span>
<span data-ttu-id="f8d2c-167">VMSS Resource Manager 템플릿 내에서 `licenseType` 에 대한 추가 매개 변수를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8d2c-167">Within your VMSS Resource Manager templates, an additional parameter for `licenseType` must be specified.</span></span> <span data-ttu-id="f8d2c-168">[Azure Resource Manager 템플릿 작성](../../resource-group-authoring-templates.md)에 대해 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8d2c-168">You can read more about [authoring Azure Resource Manager templates](../../resource-group-authoring-templates.md).</span></span> <span data-ttu-id="f8d2c-169">Hello 크기 집합 virtualMachineProfile의 일환으로 리소스 관리자 템플릿 tooinclude hello licenseType 속성을 편집 하 고 일반적인 방법으로 템플릿을 배포-2016 Windows Server 이미지를 사용 하 여 아래 예제를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="f8d2c-169">Edit your Resource Manager template tooinclude hello licenseType property as part of hello scale set’s virtualMachineProfile and deploy your template as normal - see example below using 2016 Windows Server image:</span></span>


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
> <span data-ttu-id="f8d2c-170">PowerShell 및 다른 SDK 도구를 통해 AHUB 기능을 활용하여 가상 컴퓨터 확장 집합을 배포하는 방식은 곧 지원될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="f8d2c-170">Support for deploying a virtual machine scale set with AHUB benefits through PowerShell and other SDK tools is coming soon.</span></span>
>

## <a name="next-steps"></a><span data-ttu-id="f8d2c-171">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f8d2c-171">Next steps</span></span>
<span data-ttu-id="f8d2c-172">자세한 내용은 [Azure 하이브리드 사용 혜택 라이선싱](https://azure.microsoft.com/pricing/hybrid-use-benefit/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f8d2c-172">Read more about [Azure Hybrid Use Benefit licensing](https://azure.microsoft.com/pricing/hybrid-use-benefit/).</span></span>

<span data-ttu-id="f8d2c-173">[Resource Manager 템플릿 사용](../../azure-resource-manager/resource-group-overview.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f8d2c-173">Learn more about [using Resource Manager templates](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="f8d2c-174">에 대 한 자세한 내용은 [Azure 하이브리드 사용 이점 및 Azure 사이트 복구 확인 마이그레이션 응용 프로그램 tooAzure 훨씬 더 비용 효율적인](https://azure.microsoft.com/blog/hybrid-use-benefit-migration-with-asr/)합니다.</span><span class="sxs-lookup"><span data-stu-id="f8d2c-174">Learn more about [Azure Hybrid Use Benefit and Azure Site Recovery make migrating applications tooAzure even more cost-effective](https://azure.microsoft.com/blog/hybrid-use-benefit-migration-with-asr/).</span></span>
