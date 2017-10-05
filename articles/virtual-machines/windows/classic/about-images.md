---
title: "Windows 가상 컴퓨터에 대한 이미지 정보 | Microsoft Docs"
description: "Azure에서 Windows 가상 컴퓨터와 함께 이미지를 사용하는 방법에 대해 알아봅니다."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 66ff3fab-8e7f-4dff-b8da-ab1c9c9c9af8
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: cynthn
ms.openlocfilehash: d421cee0becabdf81d865036d0c98b12b077152b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="about-images-for-windows-virtual-machines"></a><span data-ttu-id="42897-103">Windows 가상 컴퓨터에 대한 이미지 정보</span><span class="sxs-lookup"><span data-stu-id="42897-103">About images for Windows virtual machines</span></span>
> [!IMPORTANT]
> <span data-ttu-id="42897-104">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42897-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="42897-105">이 문서에서는 클래식 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="42897-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="42897-106">새로운 배포는 대부분 리소스 관리자 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="42897-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="42897-107">Resource Manager 모델의 이미지를 찾고 사용하는 방법에 대한 정보는 [여기](../../virtual-machines-windows-cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="42897-107">For information about finding and using images in the Resource Manager model, see [here](../../virtual-machines-windows-cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-classic-about-images](../../../../includes/virtual-machines-common-classic-about-images.md)]

## <a name="working-with-images"></a><span data-ttu-id="42897-108">이미지 작업</span><span class="sxs-lookup"><span data-stu-id="42897-108">Working with images</span></span>

<span data-ttu-id="42897-109">Azure PowerShell 모듈 및 Azure Portal을 사용하여 Azure 구독에 사용할 수 있는 이미지를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42897-109">You can use the Azure PowerShell module and the Azure portal to manage the images available to your Azure subscription.</span></span> <span data-ttu-id="42897-110">Azure PowerShell 모듈은 확인하거나 보려는 내용을 정확하게 겨냥할 수 있도록 더 많은 명령 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="42897-110">The Azure PowerShell module provides more command options, so you can pinpoint exactly what you want to see or do.</span></span> <span data-ttu-id="42897-111">Azure Portal은 일상적인 대부분의 관리 태스크에 대한 GUI를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="42897-111">The Azure portal provides a GUI for many of the everyday administrative tasks.</span></span>

<span data-ttu-id="42897-112">Azure PowerShell 모듈을 사용하는 몇 가지 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="42897-112">Here are some examples that use the Azure PowerShell module.</span></span>

* <span data-ttu-id="42897-113">**모든 이미지 가져오기**:`Get-AzureVMImage`현재 구독에서 사용할 수 있는 모든 이미지 목록 반환: 사용자의 이미지 및 Azure 또는 파트너에서 제공하는 이미지입니다.</span><span class="sxs-lookup"><span data-stu-id="42897-113">**Get all images**:`Get-AzureVMImage`returns a list of all the images available in your current subscription: your images and those provided by Azure or partners.</span></span> <span data-ttu-id="42897-114">결과 목록은 클 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42897-114">The resulting list could be large.</span></span> <span data-ttu-id="42897-115">다음 예에서는 짧은 목록을 가져오는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="42897-115">The next examples show how to get a shorter list.</span></span>
* <span data-ttu-id="42897-116">**이미지 제품군 가져오기**:`Get-AzureVMImage | select ImageFamily` **ImageFamily** 속성 문자열을 표시하여 이미지 제품군 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="42897-116">**Get image families**:`Get-AzureVMImage | select ImageFamily` gets a list of image families by showing strings **ImageFamily** property.</span></span>
* <span data-ttu-id="42897-117">**특정 제품군의 모든 이미지 가져오기**: `Get-AzureVMImage | Where-Object {$_.ImageFamily -eq $family}`</span><span class="sxs-lookup"><span data-stu-id="42897-117">**Get all images in a specific family**: `Get-AzureVMImage | Where-Object {$_.ImageFamily -eq $family}`</span></span>
* <span data-ttu-id="42897-118">**VM 이미지 찾기**: `Get-AzureVMImage | where {(gm –InputObject $_ -Name DataDiskConfigurations) -ne $null} | Select -Property Label, ImageName` 이 cmdlet은 VM 이미지에만 적용되는 DataDiskConfiguration 속성을 필터링하여 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="42897-118">**Find VM Images**: `Get-AzureVMImage | where {(gm –InputObject $_ -Name DataDiskConfigurations) -ne $null} | Select -Property Label, ImageName` This cmdlet works by filtering the DataDiskConfiguration property, which only applies to VM Images.</span></span> <span data-ttu-id="42897-119">또한 이 예에서는 출력을 레이블 및 이미지 이름으로만 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="42897-119">This example also filters the output to only the label and image name.</span></span>
* <span data-ttu-id="42897-120">**일반화된 이미지 저장**: `Save-AzureVMImage –ServiceName "myServiceName" –Name "MyVMtoCapture" –OSState "Generalized" –ImageName "MyVmImage" –ImageLabel "This is my generalized image"`</span><span class="sxs-lookup"><span data-stu-id="42897-120">**Save a generalized image**: `Save-AzureVMImage –ServiceName "myServiceName" –Name "MyVMtoCapture" –OSState "Generalized" –ImageName "MyVmImage" –ImageLabel "This is my generalized image"`</span></span>
* <span data-ttu-id="42897-121">**특수화된 이미지 저장**: `Save-AzureVMImage –ServiceName "mySvc2" –Name "MyVMToCapture2" –ImageName "myFirstVMImageSP" –OSState "Specialized" -Verbose`</span><span class="sxs-lookup"><span data-stu-id="42897-121">**Save a specialized image**: `Save-AzureVMImage –ServiceName "mySvc2" –Name "MyVMToCapture2" –ImageName "myFirstVMImageSP" –OSState "Specialized" -Verbose`</span></span>

  > [!TIP]
  > <span data-ttu-id="42897-122">운영 체제 디스크 및 연결된 데이터 디스크를 포함하는 VM 이미지를 만들려면 OSState 매개 변수가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="42897-122">The OSState parameter is required to create a VM image, which includes the operating system disk and attached data disks.</span></span> <span data-ttu-id="42897-123">매개 변수를 사용하지 않으면 cmdlet에서 OS 이미지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="42897-123">If you don’t use the parameter, the cmdlet creates an OS image.</span></span> <span data-ttu-id="42897-124">매개 변수의 값은 운영 체제 디스크가 다시 사용하도록 준비되어 있는지 여부에 따라 이미지가 일반화되었는지 특수화되었는지를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="42897-124">The value of the parameter indicates whether the image is generalized or specialized, based on whether the operating system disk has been prepared for reuse.</span></span>

* <span data-ttu-id="42897-125">**이미지 삭제**: `Remove-AzureVMImage –ImageName "MyOldVmImage"`</span><span class="sxs-lookup"><span data-stu-id="42897-125">**Delete an image**: `Remove-AzureVMImage –ImageName "MyOldVmImage"`</span></span>

## <a name="next-steps"></a><span data-ttu-id="42897-126">다음 단계</span><span class="sxs-lookup"><span data-stu-id="42897-126">Next Steps</span></span>
<span data-ttu-id="42897-127">또한 [Azure Portal을 사용하여 Windows 컴퓨터를 만들](tutorial.md) 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42897-127">You can also [create a Windows machine using the Azure portal](tutorial.md).</span></span>
