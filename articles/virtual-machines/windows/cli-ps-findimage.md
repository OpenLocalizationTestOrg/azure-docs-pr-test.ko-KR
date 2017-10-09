---
title: "Azure에서 이미지를 Windows VM aaaSelect | Microsoft Docs"
description: "게시자, 제품, SKU 및 마켓플레이스 VM 이미지에 대 한 버전 toouse Azure PowerSHell toodetermine hello 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 752edcd0935f5141832e49503ae800ea0145e219
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toofind-windows-vm-images-in-hello-azure-marketplace-with-azure-powershell"></a><span data-ttu-id="38f6b-103">Windows VM toofind hello Azure PowerShell을 사용한 Azure 마켓플레이스 이미지 방법</span><span class="sxs-lookup"><span data-stu-id="38f6b-103">How toofind Windows VM images in hello Azure Marketplace with Azure PowerShell</span></span>

<span data-ttu-id="38f6b-104">이 항목에서는 toouse Azure PowerShell toofind VM hello Azure 마켓플레이스 이미지 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="38f6b-104">This topic describes how toouse Azure PowerShell toofind VM images in hello Azure Marketplace.</span></span> <span data-ttu-id="38f6b-105">Windows VM을 만들 때이 정보 toospecify 마켓플레이스 이미지를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="38f6b-105">Use this information toospecify a Marketplace image when you create a Windows VM.</span></span>

<span data-ttu-id="38f6b-106">설치 하 고 최신 hello 구성 되었는지 확인 [Azure PowerShell 모듈](/powershell/azure/install-azurerm-ps)합니다.</span><span class="sxs-lookup"><span data-stu-id="38f6b-106">Make sure that you installed and configured hello latest [Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>



## <a name="table-of-commonly-used-windows-images"></a><span data-ttu-id="38f6b-107">일반적으로 사용하는 Windows 이미지 테이블</span><span class="sxs-lookup"><span data-stu-id="38f6b-107">Table of commonly used Windows images</span></span>
| <span data-ttu-id="38f6b-108">PublisherName</span><span class="sxs-lookup"><span data-stu-id="38f6b-108">PublisherName</span></span> | <span data-ttu-id="38f6b-109">제안</span><span class="sxs-lookup"><span data-stu-id="38f6b-109">Offer</span></span> | <span data-ttu-id="38f6b-110">SKU</span><span class="sxs-lookup"><span data-stu-id="38f6b-110">Sku</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="38f6b-111">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="38f6b-111">MicrosoftWindowsServer</span></span> |<span data-ttu-id="38f6b-112">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="38f6b-112">WindowsServer</span></span> |<span data-ttu-id="38f6b-113">2016-Datacenter</span><span class="sxs-lookup"><span data-stu-id="38f6b-113">2016-Datacenter</span></span> |
| <span data-ttu-id="38f6b-114">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="38f6b-114">MicrosoftWindowsServer</span></span> |<span data-ttu-id="38f6b-115">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="38f6b-115">WindowsServer</span></span> |<span data-ttu-id="38f6b-116">2016-Datacenter-Server-Core</span><span class="sxs-lookup"><span data-stu-id="38f6b-116">2016-Datacenter-Server-Core</span></span> |
| <span data-ttu-id="38f6b-117">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="38f6b-117">MicrosoftWindowsServer</span></span> |<span data-ttu-id="38f6b-118">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="38f6b-118">WindowsServer</span></span> |<span data-ttu-id="38f6b-119">2016-Datacenter-with-Containers</span><span class="sxs-lookup"><span data-stu-id="38f6b-119">2016-Datacenter-with-Containers</span></span> |
| <span data-ttu-id="38f6b-120">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="38f6b-120">MicrosoftWindowsServer</span></span> |<span data-ttu-id="38f6b-121">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="38f6b-121">WindowsServer</span></span> |<span data-ttu-id="38f6b-122">2016-Nano-Server</span><span class="sxs-lookup"><span data-stu-id="38f6b-122">2016-Nano-Server</span></span> |
| <span data-ttu-id="38f6b-123">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="38f6b-123">MicrosoftWindowsServer</span></span> |<span data-ttu-id="38f6b-124">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="38f6b-124">WindowsServer</span></span> |<span data-ttu-id="38f6b-125">2012-R2-Datacenter</span><span class="sxs-lookup"><span data-stu-id="38f6b-125">2012-R2-Datacenter</span></span> |
| <span data-ttu-id="38f6b-126">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="38f6b-126">MicrosoftWindowsServer</span></span> |<span data-ttu-id="38f6b-127">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="38f6b-127">WindowsServer</span></span> |<span data-ttu-id="38f6b-128">2008-R2-SP1</span><span class="sxs-lookup"><span data-stu-id="38f6b-128">2008-R2-SP1</span></span> |
| <span data-ttu-id="38f6b-129">MicrosoftDynamicsNAV</span><span class="sxs-lookup"><span data-stu-id="38f6b-129">MicrosoftDynamicsNAV</span></span> |<span data-ttu-id="38f6b-130">DynamicsNAV</span><span class="sxs-lookup"><span data-stu-id="38f6b-130">DynamicsNAV</span></span> |<span data-ttu-id="38f6b-131">2017</span><span class="sxs-lookup"><span data-stu-id="38f6b-131">2017</span></span> |
| <span data-ttu-id="38f6b-132">MicrosoftSharePoint</span><span class="sxs-lookup"><span data-stu-id="38f6b-132">MicrosoftSharePoint</span></span> |<span data-ttu-id="38f6b-133">MicrosoftSharePointServer</span><span class="sxs-lookup"><span data-stu-id="38f6b-133">MicrosoftSharePointServer</span></span> |<span data-ttu-id="38f6b-134">2016</span><span class="sxs-lookup"><span data-stu-id="38f6b-134">2016</span></span> |
| <span data-ttu-id="38f6b-135">MicrosoftSQLServer</span><span class="sxs-lookup"><span data-stu-id="38f6b-135">MicrosoftSQLServer</span></span> |<span data-ttu-id="38f6b-136">SQL2016-WS2016</span><span class="sxs-lookup"><span data-stu-id="38f6b-136">SQL2016-WS2016</span></span> |<span data-ttu-id="38f6b-137">Enterprise</span><span class="sxs-lookup"><span data-stu-id="38f6b-137">Enterprise</span></span> |
| <span data-ttu-id="38f6b-138">MicrosoftSQLServer</span><span class="sxs-lookup"><span data-stu-id="38f6b-138">MicrosoftSQLServer</span></span> |<span data-ttu-id="38f6b-139">SQL2014SP2-WS2012R2</span><span class="sxs-lookup"><span data-stu-id="38f6b-139">SQL2014SP2-WS2012R2</span></span> |<span data-ttu-id="38f6b-140">Enterprise</span><span class="sxs-lookup"><span data-stu-id="38f6b-140">Enterprise</span></span> |
| <span data-ttu-id="38f6b-141">MicrosoftWindowsServerHPCPack</span><span class="sxs-lookup"><span data-stu-id="38f6b-141">MicrosoftWindowsServerHPCPack</span></span> |<span data-ttu-id="38f6b-142">WindowsServerHPCPack</span><span class="sxs-lookup"><span data-stu-id="38f6b-142">WindowsServerHPCPack</span></span> |<span data-ttu-id="38f6b-143">2012R2</span><span class="sxs-lookup"><span data-stu-id="38f6b-143">2012R2</span></span> |
| <span data-ttu-id="38f6b-144">MicrosoftWindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="38f6b-144">MicrosoftWindowsServerEssentials</span></span> |<span data-ttu-id="38f6b-145">WindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="38f6b-145">WindowsServerEssentials</span></span> |<span data-ttu-id="38f6b-146">WindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="38f6b-146">WindowsServerEssentials</span></span> |

## <a name="find-specific-images"></a><span data-ttu-id="38f6b-147">특정 이미지 찾기</span><span class="sxs-lookup"><span data-stu-id="38f6b-147">Find specific images</span></span>


<span data-ttu-id="38f6b-148">새 가상 컴퓨터를 Azure 리소스 관리자를 만들 때 일부 경우에 필요 toospecify 이미지를 다음과 같은 이미지 속성 hello hello 결합 합니다.</span><span class="sxs-lookup"><span data-stu-id="38f6b-148">When creating a new virtual machine with Azure Resource Manager, in some cases you need toospecify an image with hello combination of hello following image properties:</span></span>

* <span data-ttu-id="38f6b-149">게시자</span><span class="sxs-lookup"><span data-stu-id="38f6b-149">Publisher</span></span>
* <span data-ttu-id="38f6b-150">제안</span><span class="sxs-lookup"><span data-stu-id="38f6b-150">Offer</span></span>
* <span data-ttu-id="38f6b-151">SKU</span><span class="sxs-lookup"><span data-stu-id="38f6b-151">SKU</span></span>

<span data-ttu-id="38f6b-152">예를 들어, 이러한 값을 사용 하 여 hello로 [집합 AzureRMVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) PowerShell cmdlet 또는 리소스 그룹 템플릿을 만든 VM toobe 유형의 hello를 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="38f6b-152">For example, use these values with hello [Set-AzureRMVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) PowerShell cmdlet, or with a resource group template in which you must specify hello type of VM toobe created.</span></span>

<span data-ttu-id="38f6b-153">이러한 값 toodetermine 해야 할 경우 hello를 실행할 수 있습니다 [Get AzureRMVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher), [Get AzureRMVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer), 및 [Get AzureRMVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) cmdlet toonavigate hello 이미지입니다.</span><span class="sxs-lookup"><span data-stu-id="38f6b-153">If you need toodetermine these values, you can run hello [Get-AzureRMVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher), [Get-AzureRMVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer), and [Get-AzureRMVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) cmdlets toonavigate hello images.</span></span> <span data-ttu-id="38f6b-154">다음 값을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="38f6b-154">You determine these values:</span></span>

1. <span data-ttu-id="38f6b-155">Hello 이미지 게시자 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="38f6b-155">List hello image publishers.</span></span>
2. <span data-ttu-id="38f6b-156">지정된 게시자에 제안을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="38f6b-156">For a given publisher, list their offers.</span></span>
3. <span data-ttu-id="38f6b-157">지정된 제안에 SKU를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="38f6b-157">For a given offer, list their SKUs.</span></span>

<span data-ttu-id="38f6b-158">다음 명령 hello로 hello 게시자를 먼저 나열:</span><span class="sxs-lookup"><span data-stu-id="38f6b-158">First, list hello publishers with hello following commands:</span></span>

```powershell
$locName="<Azure location, such as West US>"
Get-AzureRMVMImagePublisher -Location $locName | Select PublisherName
```

<span data-ttu-id="38f6b-159">선택한 게시자 이름을 입력 하 고 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="38f6b-159">Fill in your chosen publisher name and run hello following commands:</span></span>

```powershell
$pubName="<publisher>"
Get-AzureRMVMImageOffer -Location $locName -Publisher $pubName | Select Offer
```

<span data-ttu-id="38f6b-160">선택한 제품 이름에 입력 하 고 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="38f6b-160">Fill in your chosen offer name and run hello following commands:</span></span>

```powershell
$offerName="<offer>"
Get-AzureRMVMImageSku -Location $locName -Publisher $pubName -Offer $offerName | Select Skus
```

<span data-ttu-id="38f6b-161">Hello의 hello 출력에서 `Get-AzureRMVMImageSku` 명령, toospecify hello 이미지는 새 가상 컴퓨터에 필요한 모든 hello 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="38f6b-161">From hello output of hello `Get-AzureRMVMImageSku` command, you have all hello information you need toospecify hello image for a new virtual machine.</span></span>

<span data-ttu-id="38f6b-162">hello 다음 전체 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="38f6b-162">hello following shows a full example:</span></span>

```powershell
$locName="West US"
Get-AzureRMVMImagePublisher -Location $locName | Select PublisherName

```

<span data-ttu-id="38f6b-163">출력:</span><span class="sxs-lookup"><span data-stu-id="38f6b-163">Output:</span></span>

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

<span data-ttu-id="38f6b-164">Hello "MicrosoftWindowsServer" 게시자:</span><span class="sxs-lookup"><span data-stu-id="38f6b-164">For hello "MicrosoftWindowsServer" publisher:</span></span>

```powershell
$pubName="MicrosoftWindowsServer"
Get-AzureRMVMImageOffer -Location $locName -Publisher $pubName | Select Offer
```

<span data-ttu-id="38f6b-165">출력:</span><span class="sxs-lookup"><span data-stu-id="38f6b-165">Output:</span></span>

```
Offer
-----
Windows-HUB
WindowsServer
WindowsServer-HUB
```

<span data-ttu-id="38f6b-166">"Windows Server" hello에 대 한 다음을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="38f6b-166">For hello "WindowsServer" offer:</span></span>

```powershell
$offerName="WindowsServer"
Get-AzureRMVMImageSku -Location $locName -Publisher $pubName -Offer $offerName | Select Skus
```

<span data-ttu-id="38f6b-167">출력:</span><span class="sxs-lookup"><span data-stu-id="38f6b-167">Output:</span></span>

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

<span data-ttu-id="38f6b-168">SKU 이름을 선택 하는 hello 복사한 hello에 대 한 모든 hello 정보가 있으면이 목록에서 `Set-AzureRMVMSourceImage` PowerShell cmdlet 또는 리소스 그룹 템플릿에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="38f6b-168">From this list, copy hello chosen SKU name, and you have all hello information for hello `Set-AzureRMVMSourceImage` PowerShell cmdlet or for a resource group template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="38f6b-169">다음 단계</span><span class="sxs-lookup"><span data-stu-id="38f6b-169">Next steps</span></span>
<span data-ttu-id="38f6b-170">정확 하 게 hello 이미지를 선택할 수 이제 toouse를 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="38f6b-170">Now you can choose precisely hello image you want toouse.</span></span> <span data-ttu-id="38f6b-171">toocreate 가상 컴퓨터를 찾을 수 있는 hello 이미지 정보를 사용 하 여 신속 하 게 참조 [PowerShell을 사용한 Windows 가상 컴퓨터를 만들](quick-create-powershell.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="38f6b-171">toocreate a virtual machine quickly by using hello image information, which you just found, see [Create a Windows virtual machine with PowerShell](quick-create-powershell.md).</span></span>
