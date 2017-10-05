---
title: "PowerShell을 사용하여 Azure DevTest Labs에 VHD 파일 업로드 | Microsoft Docs"
description: "PowerShell을 사용하여 랩의 저장소 계정에 VHD 파일 업로드"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 3c43ef77b8fa10cd6dbd726968264f32f7a3dd0f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="upload-vhd-file-to-labs-storage-account-using-powershell"></a><span data-ttu-id="81415-103">PowerShell을 사용하여 랩의 저장소 계정에 VHD 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="81415-103">Upload VHD file to lab's storage account using PowerShell</span></span>

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

<span data-ttu-id="81415-104">Azure DevTest Labs에서는 VHD 파일을 사용하여 가상 컴퓨터를 프로비저닝을 사용하는 데 사용하는 사용자 지정 이미지를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81415-104">In Azure DevTest Labs, VHD files can be used to create custom images, which are used to provision virtual machines.</span></span> <span data-ttu-id="81415-105">다음 단계는 PowerShell을 사용하여 VHD 파일을 랩의 저장소 계정에 업로드하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="81415-105">The following steps walk you through using PowerShell to upload a VHD file to a lab's storage account.</span></span> <span data-ttu-id="81415-106">VHD 파일을 업로드하면 [다음 단계 섹션](#next-steps)은 업로드된 VHD 파일에서 사용자 지정 이미지를 만드는 방법을 자세히 설명하는 일부 문서를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="81415-106">Once you've uploaded your VHD file, the [Next steps section](#next-steps) lists some articles that illustrate how to create a custom image from the uploaded VHD file.</span></span> <span data-ttu-id="81415-107">Azure의 디스크 및 VHD에 대한 자세한 내용은 [가상 컴퓨터용 디스크 및 VHD 정보](../virtual-machines/linux/about-disks-and-vhds.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="81415-107">For more information about disks and VHDs in Azure, see [About disks and VHDs for virtual machines](../virtual-machines/linux/about-disks-and-vhds.md)</span></span>

## <a name="step-by-step-instructions"></a><span data-ttu-id="81415-108">단계별 지침</span><span class="sxs-lookup"><span data-stu-id="81415-108">Step-by-step instructions</span></span>

<span data-ttu-id="81415-109">다음 단계는 PowerShell을 사용하여 Azure DevTest Labs로 VHD 파일을 업로드하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="81415-109">The following steps walk you through uploading a VHD file to Azure DevTest Labs using PowerShell.</span></span> 

1. <span data-ttu-id="81415-110">[Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="81415-110">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="81415-111">**추가 서비스**를 선택한 후 목록에서 **DevTest Labs**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="81415-111">Select **More services**, and then select **DevTest Labs** from the list.</span></span>

1. <span data-ttu-id="81415-112">랩 목록에서 원하는 랩을 탭합니다.</span><span class="sxs-lookup"><span data-stu-id="81415-112">From the list of labs, select the desired lab.</span></span>  

1. <span data-ttu-id="81415-113">랩의 블레이드에서 **구성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="81415-113">On the lab's blade, select **Configuration**.</span></span> 

1. <span data-ttu-id="81415-114">랩의 **구성** 블레이드에서 **사용자 지정 이미지(VHD)**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="81415-114">On the lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>

1. <span data-ttu-id="81415-115">**사용자 지정 이미지** 블레이드에서 **+추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="81415-115">On the **Custom images** blade, Select **+Add**.</span></span> 

1. <span data-ttu-id="81415-116">**사용자 지정 이미지** 블레이드에서 **VHD**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="81415-116">On the **Custom image** blade, select **VHD**.</span></span>

1. <span data-ttu-id="81415-117">**VHD** 블레이드에서 **PowerShell을 사용하여 VHD 업로드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="81415-117">On the **VHD** blade, select **Upload a VHD using PowerShell**.</span></span>

    ![PowerShell을 사용하여 VHD 업로드](./media/devtest-lab-upload-vhd-using-powershell/upload-image-using-psh.png)

1. <span data-ttu-id="81415-119">**PowerShell을 사용하여 이미지 업로드** 블레이드에서 생성된 PowerShell 스크립트를 텍스트 편집기에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="81415-119">On the **Upload an image using PowerShell** blade, copy the generated PowerShell script to a text editor.</span></span>

1. <span data-ttu-id="81415-120">**Add-AzureVhd** cmdlet의 **LocalFilePath** 매개 변수를 수정하여 업로드하려는 VHD 파일의 위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="81415-120">Modify the **LocalFilePath** parameter of the **Add-AzureVhd** cmdlet to point to the location of the VHD file you want to upload.</span></span>

1. <span data-ttu-id="81415-121">PowerShell 프롬프트에서 **Add-AzureVhd** cmdlet(수정된 **LocalFilePath** 매개 변수 포함)을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="81415-121">At a PowerShell prompt, run the **Add-AzureVhd** cmdlet (with the modified **LocalFilePath** parameter).</span></span>

> [!WARNING] 
> 
> <span data-ttu-id="81415-122">VHD 파일을 업로드하는 프로세스는 VHD 파일 크기 및 연결 속도에 따라 시간이 오래 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81415-122">The process of uploading a VHD file can be lengthy depending on the size of the VHD file and your connection speed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="81415-123">다음 단계</span><span class="sxs-lookup"><span data-stu-id="81415-123">Next steps</span></span>

- [<span data-ttu-id="81415-124">Azure Portal을 사용하여 VHD 파일에서 Azure DevTest Labs에 사용자 지정 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="81415-124">Create a custom image in Azure DevTest Labs from a VHD file using the Azure portal</span></span>](devtest-lab-create-template.md)
- [<span data-ttu-id="81415-125">PowerShell을 사용하여 VHD 파일에서 Azure DevTest Labs에 사용자 지정 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="81415-125">Create a custom image in Azure DevTest Labs from a VHD file using PowerShell</span></span>](devtest-lab-create-custom-image-from-vhd-using-powershell.md)
