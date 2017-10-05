---
title: "Azure에서 Windows VM 이미지 선택 | Microsoft Docs"
description: "Azure PowerSHell을 사용하여 Marketplace VM 이미지의 게시자, 제품, SKU 및 버전을 확인하는 방법을 알아봅니다."
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 188b8974-fabd-4cd3-b7dc-559cbb86b98a
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/12/2017
ms.author: danlep
ms.openlocfilehash: 814ae260123c045d4b6766bf4b312f874cd77068
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-find-windows-vm-images-in-the-azure-marketplace-with-azure-powershell"></a><span data-ttu-id="e8958-103">Azure PowerShell을 사용하여 Azure Marketplace에서 Windows VM 이미지를 찾는 방법</span><span class="sxs-lookup"><span data-stu-id="e8958-103">How to find Windows VM images in the Azure Marketplace with Azure PowerShell</span></span>

<span data-ttu-id="e8958-104">이 항목에서는 Azure PowerShell을 사용하여 Azure Marketplace에서 VM 이미지를 찾는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e8958-104">This topic describes how to use Azure PowerShell to find VM images in the Azure Marketplace.</span></span> <span data-ttu-id="e8958-105">이 정보를 사용하여 Windows VM을 만들 때 Marketplace 이미지를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e8958-105">Use this information to specify a Marketplace image when you create a Windows VM.</span></span>

<span data-ttu-id="e8958-106">최신 [Azure PowerShell 모듈](/powershell/azure/install-azurerm-ps)을 설치 및 구성했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e8958-106">Make sure that you installed and configured the latest [Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>



## <a name="table-of-commonly-used-windows-images"></a><span data-ttu-id="e8958-107">일반적으로 사용하는 Windows 이미지 테이블</span><span class="sxs-lookup"><span data-stu-id="e8958-107">Table of commonly used Windows images</span></span>
| <span data-ttu-id="e8958-108">PublisherName</span><span class="sxs-lookup"><span data-stu-id="e8958-108">PublisherName</span></span> | <span data-ttu-id="e8958-109">제안</span><span class="sxs-lookup"><span data-stu-id="e8958-109">Offer</span></span> | <span data-ttu-id="e8958-110">SKU</span><span class="sxs-lookup"><span data-stu-id="e8958-110">Sku</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="e8958-111">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="e8958-111">MicrosoftWindowsServer</span></span> |<span data-ttu-id="e8958-112">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="e8958-112">WindowsServer</span></span> |<span data-ttu-id="e8958-113">2016-Datacenter</span><span class="sxs-lookup"><span data-stu-id="e8958-113">2016-Datacenter</span></span> |
| <span data-ttu-id="e8958-114">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="e8958-114">MicrosoftWindowsServer</span></span> |<span data-ttu-id="e8958-115">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="e8958-115">WindowsServer</span></span> |<span data-ttu-id="e8958-116">2016-Datacenter-Server-Core</span><span class="sxs-lookup"><span data-stu-id="e8958-116">2016-Datacenter-Server-Core</span></span> |
| <span data-ttu-id="e8958-117">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="e8958-117">MicrosoftWindowsServer</span></span> |<span data-ttu-id="e8958-118">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="e8958-118">WindowsServer</span></span> |<span data-ttu-id="e8958-119">2016-Datacenter-with-Containers</span><span class="sxs-lookup"><span data-stu-id="e8958-119">2016-Datacenter-with-Containers</span></span> |
| <span data-ttu-id="e8958-120">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="e8958-120">MicrosoftWindowsServer</span></span> |<span data-ttu-id="e8958-121">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="e8958-121">WindowsServer</span></span> |<span data-ttu-id="e8958-122">2016-Nano-Server</span><span class="sxs-lookup"><span data-stu-id="e8958-122">2016-Nano-Server</span></span> |
| <span data-ttu-id="e8958-123">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="e8958-123">MicrosoftWindowsServer</span></span> |<span data-ttu-id="e8958-124">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="e8958-124">WindowsServer</span></span> |<span data-ttu-id="e8958-125">2012-R2-Datacenter</span><span class="sxs-lookup"><span data-stu-id="e8958-125">2012-R2-Datacenter</span></span> |
| <span data-ttu-id="e8958-126">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="e8958-126">MicrosoftWindowsServer</span></span> |<span data-ttu-id="e8958-127">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="e8958-127">WindowsServer</span></span> |<span data-ttu-id="e8958-128">2008-R2-SP1</span><span class="sxs-lookup"><span data-stu-id="e8958-128">2008-R2-SP1</span></span> |
| <span data-ttu-id="e8958-129">MicrosoftDynamicsNAV</span><span class="sxs-lookup"><span data-stu-id="e8958-129">MicrosoftDynamicsNAV</span></span> |<span data-ttu-id="e8958-130">DynamicsNAV</span><span class="sxs-lookup"><span data-stu-id="e8958-130">DynamicsNAV</span></span> |<span data-ttu-id="e8958-131">2017</span><span class="sxs-lookup"><span data-stu-id="e8958-131">2017</span></span> |
| <span data-ttu-id="e8958-132">MicrosoftSharePoint</span><span class="sxs-lookup"><span data-stu-id="e8958-132">MicrosoftSharePoint</span></span> |<span data-ttu-id="e8958-133">MicrosoftSharePointServer</span><span class="sxs-lookup"><span data-stu-id="e8958-133">MicrosoftSharePointServer</span></span> |<span data-ttu-id="e8958-134">2016</span><span class="sxs-lookup"><span data-stu-id="e8958-134">2016</span></span> |
| <span data-ttu-id="e8958-135">MicrosoftSQLServer</span><span class="sxs-lookup"><span data-stu-id="e8958-135">MicrosoftSQLServer</span></span> |<span data-ttu-id="e8958-136">SQL2016-WS2016</span><span class="sxs-lookup"><span data-stu-id="e8958-136">SQL2016-WS2016</span></span> |<span data-ttu-id="e8958-137">Enterprise</span><span class="sxs-lookup"><span data-stu-id="e8958-137">Enterprise</span></span> |
| <span data-ttu-id="e8958-138">MicrosoftSQLServer</span><span class="sxs-lookup"><span data-stu-id="e8958-138">MicrosoftSQLServer</span></span> |<span data-ttu-id="e8958-139">SQL2014SP2-WS2012R2</span><span class="sxs-lookup"><span data-stu-id="e8958-139">SQL2014SP2-WS2012R2</span></span> |<span data-ttu-id="e8958-140">Enterprise</span><span class="sxs-lookup"><span data-stu-id="e8958-140">Enterprise</span></span> |
| <span data-ttu-id="e8958-141">MicrosoftWindowsServerHPCPack</span><span class="sxs-lookup"><span data-stu-id="e8958-141">MicrosoftWindowsServerHPCPack</span></span> |<span data-ttu-id="e8958-142">WindowsServerHPCPack</span><span class="sxs-lookup"><span data-stu-id="e8958-142">WindowsServerHPCPack</span></span> |<span data-ttu-id="e8958-143">2012R2</span><span class="sxs-lookup"><span data-stu-id="e8958-143">2012R2</span></span> |
| <span data-ttu-id="e8958-144">MicrosoftWindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="e8958-144">MicrosoftWindowsServerEssentials</span></span> |<span data-ttu-id="e8958-145">WindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="e8958-145">WindowsServerEssentials</span></span> |<span data-ttu-id="e8958-146">WindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="e8958-146">WindowsServerEssentials</span></span> |

## <a name="find-specific-images"></a><span data-ttu-id="e8958-147">특정 이미지 찾기</span><span class="sxs-lookup"><span data-stu-id="e8958-147">Find specific images</span></span>


<span data-ttu-id="e8958-148">Azure 리소스 관리자를 사용하여 새 가상 컴퓨터를 만들 때 다음 이미지 속성을 조합하여 이미지를 지정해야 하는 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8958-148">When creating a new virtual machine with Azure Resource Manager, in some cases you need to specify an image with the combination of the following image properties:</span></span>

* <span data-ttu-id="e8958-149">게시자</span><span class="sxs-lookup"><span data-stu-id="e8958-149">Publisher</span></span>
* <span data-ttu-id="e8958-150">제안</span><span class="sxs-lookup"><span data-stu-id="e8958-150">Offer</span></span>
* <span data-ttu-id="e8958-151">SKU</span><span class="sxs-lookup"><span data-stu-id="e8958-151">SKU</span></span>

<span data-ttu-id="e8958-152">예를 들어 [Set-AzureRMVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) PowerShell cmdlet 또는 만든 VM 유형을 지정해야 하는 리소스 그룹 템플릿에서 이러한 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e8958-152">For example, use these values with the [Set-AzureRMVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) PowerShell cmdlet, or with a resource group template in which you must specify the type of VM to be created.</span></span>

<span data-ttu-id="e8958-153">이러한 값을 확인해야 할 경우 [Get-AzureRMVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher), [Get-AzureRMVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer) 및 [Get-AzureRMVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku)를 실행하여 이미지를 탐색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8958-153">If you need to determine these values, you can run the [Get-AzureRMVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher), [Get-AzureRMVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer), and [Get-AzureRMVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) cmdlets to navigate the images.</span></span> <span data-ttu-id="e8958-154">다음 값을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e8958-154">You determine these values:</span></span>

1. <span data-ttu-id="e8958-155">이미지 게시자를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="e8958-155">List the image publishers.</span></span>
2. <span data-ttu-id="e8958-156">지정된 게시자에 제안을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="e8958-156">For a given publisher, list their offers.</span></span>
3. <span data-ttu-id="e8958-157">지정된 제안에 SKU를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="e8958-157">For a given offer, list their SKUs.</span></span>

<span data-ttu-id="e8958-158">먼저 다음 명령을 사용하여 게시자를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="e8958-158">First, list the publishers with the following commands:</span></span>

```powershell
$locName="<Azure location, such as West US>"
Get-AzureRMVMImagePublisher -Location $locName | Select PublisherName
```

<span data-ttu-id="e8958-159">선택한 게시자 이름을 입력하고 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e8958-159">Fill in your chosen publisher name and run the following commands:</span></span>

```powershell
$pubName="<publisher>"
Get-AzureRMVMImageOffer -Location $locName -Publisher $pubName | Select Offer
```

<span data-ttu-id="e8958-160">선택한 제품 이름을 입력하고 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e8958-160">Fill in your chosen offer name and run the following commands:</span></span>

```powershell
$offerName="<offer>"
Get-AzureRMVMImageSku -Location $locName -Publisher $pubName -Offer $offerName | Select Skus
```

<span data-ttu-id="e8958-161">`Get-AzureRMVMImageSku` 명령 출력에 새 가상 컴퓨터에 대한 이미지를 지정하는 데 필요한 모든 정보가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8958-161">From the output of the `Get-AzureRMVMImageSku` command, you have all the information you need to specify the image for a new virtual machine.</span></span>

<span data-ttu-id="e8958-162">전체 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e8958-162">The following shows a full example:</span></span>

```powershell
$locName="West US"
Get-AzureRMVMImagePublisher -Location $locName | Select PublisherName

```

<span data-ttu-id="e8958-163">출력:</span><span class="sxs-lookup"><span data-stu-id="e8958-163">Output:</span></span>

```
PublisherName
-------------
a10networks
aiscaler-cache-control-ddos-and-url-rewriting-
alertlogic
AlertLogic.Extension
Barracuda.Azure.ConnectivityAgent
barracudanetworks
basho
boxless
bssw
Canonical
...
```

<span data-ttu-id="e8958-164">게시자가 "MicrosoftWindowsServer"인 경우:</span><span class="sxs-lookup"><span data-stu-id="e8958-164">For the "MicrosoftWindowsServer" publisher:</span></span>

```powershell
$pubName="MicrosoftWindowsServer"
Get-AzureRMVMImageOffer -Location $locName -Publisher $pubName | Select Offer
```

<span data-ttu-id="e8958-165">출력:</span><span class="sxs-lookup"><span data-stu-id="e8958-165">Output:</span></span>

```
Offer
-----
Windows-HUB
WindowsServer
WindowsServer-HUB
```

<span data-ttu-id="e8958-166">"WindowsServer" 제품인 경우:</span><span class="sxs-lookup"><span data-stu-id="e8958-166">For the "WindowsServer" offer:</span></span>

```powershell
$offerName="WindowsServer"
Get-AzureRMVMImageSku -Location $locName -Publisher $pubName -Offer $offerName | Select Skus
```

<span data-ttu-id="e8958-167">출력:</span><span class="sxs-lookup"><span data-stu-id="e8958-167">Output:</span></span>

```
Skus
----
2008-R2-SP1
2008-R2-SP1-smalldisk
2012-Datacenter
2012-Datacenter-smalldisk
2012-R2-Datacenter
2012-R2-Datacenter-smalldisk
2016-Datacenter
2016-Datacenter-Server-Core
2016-Datacenter-Server-Core-smalldisk
2016-Datacenter-smalldisk
2016-Datacenter-with-Containers
2016-Nano-Server
```

<span data-ttu-id="e8958-168">이 목록에서 선택한 SKU 이름을 복사합니다. 그러면 `Set-AzureRMVMSourceImage` PowerShell cmdlet 또는 리소스 그룹 템플릿에 대한 모든 정보를 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8958-168">From this list, copy the chosen SKU name, and you have all the information for the `Set-AzureRMVMSourceImage` PowerShell cmdlet or for a resource group template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e8958-169">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e8958-169">Next steps</span></span>
<span data-ttu-id="e8958-170">이제 사용할 이미지를 정밀하게 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8958-170">Now you can choose precisely the image you want to use.</span></span> <span data-ttu-id="e8958-171">방금 찾은 이미지 정보를 사용하여 가상 컴퓨터를 빠르게 만들려면 [PowerShell을 사용하여 Windows 가상 컴퓨터 만들기](quick-create-powershell.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e8958-171">To create a virtual machine quickly by using the image information, which you just found, see [Create a Windows virtual machine with PowerShell](quick-create-powershell.md).</span></span>
