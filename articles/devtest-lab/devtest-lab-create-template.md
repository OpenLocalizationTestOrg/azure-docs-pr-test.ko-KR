---
title: "VHD 파일에서 Azure DevTest Labs 사용자 지정 이미지 만들기 | Microsoft Docs"
description: "Azure Portal을 사용하여 VHD 파일에서 Azure DevTest Labs에 사용자 지정 이미지를 만드는 방법에 대해 알아봅니다."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: b795bc61-7c28-40e6-82fc-96d629ee0568
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 9983ea9b847f44ed18a6169a4bdb224b63626a64
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-custom-image-from-a-vhd-file"></a><span data-ttu-id="4d99f-103">VHD 파일에서 사용자 지정 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="4d99f-103">Create a custom image from a VHD file</span></span>

[!INCLUDE [devtest-lab-create-custom-image-from-vhd-selector](../../includes/devtest-lab-create-custom-image-from-vhd-selector.md)]

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

[!INCLUDE [devtest-lab-upload-vhd-options](../../includes/devtest-lab-upload-vhd-options.md)]

## <a name="step-by-step-instructions"></a><span data-ttu-id="4d99f-104">단계별 지침</span><span class="sxs-lookup"><span data-stu-id="4d99f-104">Step-by-step instructions</span></span>

<span data-ttu-id="4d99f-105">다음 단계는 Azure Portal을 사용하여 VHD 파일에서 사용자 지정 이미지를 만드는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="4d99f-105">The following steps walk you through creating a custom image from a VHD file using the Azure portal:</span></span>

1. <span data-ttu-id="4d99f-106">[Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="4d99f-106">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="4d99f-107">**추가 서비스**를 선택한 후 목록에서 **DevTest Labs**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4d99f-107">Select **More services**, and then select **DevTest Labs** from the list.</span></span>

1. <span data-ttu-id="4d99f-108">랩 목록에서 원하는 랩을 탭합니다.</span><span class="sxs-lookup"><span data-stu-id="4d99f-108">From the list of labs, select the desired lab.</span></span>  

1. <span data-ttu-id="4d99f-109">랩의 블레이드에서 **구성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4d99f-109">On the lab's blade, select **Configuration**.</span></span> 

1. <span data-ttu-id="4d99f-110">랩의 **구성** 블레이드에서 **사용자 지정 이미지(VHD)**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4d99f-110">On the lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>

1. <span data-ttu-id="4d99f-111">**사용자 지정 이미지** 블레이드에서 **+추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4d99f-111">On the **Custom images** blade, select **+Add**.</span></span>

    ![사용자 지정 이미지 추가](./media/devtest-lab-create-template/add-custom-image.png)

1. <span data-ttu-id="4d99f-113">사용자 지정 이미지의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4d99f-113">Enter the name of the custom image.</span></span> <span data-ttu-id="4d99f-114">이 이름은 VM을 만들 때 기본 이미지 목록에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d99f-114">This name is displayed in the list of base images when creating a VM.</span></span>

1. <span data-ttu-id="4d99f-115">사용자 지정 이미지에 대한 설명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4d99f-115">Enter the description of the custom image.</span></span> <span data-ttu-id="4d99f-116">이 설명은 VM을 만들 때 기본 이미지 목록에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d99f-116">This description is displayed in the list of base images when creating a VM.</span></span>

1. <span data-ttu-id="4d99f-117">**VHD**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4d99f-117">Select **VHD**.</span></span>

1. <span data-ttu-id="4d99f-118">**VHD** 블레이드에서 원하는 VHD 파일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4d99f-118">From the **VHD** blade, select the desired VHD file.</span></span>

1. <span data-ttu-id="4d99f-119">**확인**을 선택하여 **VHD** 블레이드를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="4d99f-119">Select **OK** to close the **VHD** blade.</span></span>

1. <span data-ttu-id="4d99f-120">**OS 구성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4d99f-120">Select **OS configuration**.</span></span>

1. <span data-ttu-id="4d99f-121">**OS 구성** 탭에서 **Windows** 또는 **Linux**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4d99f-121">On the **OS configuration** tab, select either **Windows** or **Linux**.</span></span>

1. <span data-ttu-id="4d99f-122">**Windows** 가 선택되면 확인란을 통해 컴퓨터에서 *Sysprep* 이 실행되었는지를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4d99f-122">If **Windows** is selected, specify via the checkbox whether *Sysprep* has been run on the machine.</span></span> 

1. <span data-ttu-id="4d99f-123">**확인**을 선택하여 **OS 구성** 블레이드를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="4d99f-123">Select **OK** to close the **OS configuration** blade.</span></span>

1. <span data-ttu-id="4d99f-124">**확인** 을 선택하여 사용자 지정 이미지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4d99f-124">Select **OK** to create the custom image.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="4d99f-125">관련 블로그 게시물</span><span class="sxs-lookup"><span data-stu-id="4d99f-125">Related blog posts</span></span>

- [<span data-ttu-id="4d99f-126">사용자 지정 이미지 또는 수식?</span><span class="sxs-lookup"><span data-stu-id="4d99f-126">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [<span data-ttu-id="4d99f-127">Azure DevTest Labs 간의 사용자 지정 이미지 복사</span><span class="sxs-lookup"><span data-stu-id="4d99f-127">Copying Custom Images between Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a><span data-ttu-id="4d99f-128">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4d99f-128">Next steps</span></span>

- [<span data-ttu-id="4d99f-129">랩에 VM 추가</span><span class="sxs-lookup"><span data-stu-id="4d99f-129">Add a VM to your lab</span></span>](./devtest-lab-add-vm-with-artifacts.md)
