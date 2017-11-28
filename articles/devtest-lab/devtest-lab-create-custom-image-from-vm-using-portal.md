---
title: "VHD에서 Azure DevTest Labs 사용자 지정 이미지 만들기 | Microsoft Docs"
description: "Azure Portal을 사용하여 프로비저닝된 VM에서 Azure DevTest Labs에 사용자 지정 이미지를 만드는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 9d2dcf7164985508d691e8a0c123efaf3b8aa19a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-custom-image-from-a-vm"></a><span data-ttu-id="24d43-103">VM에서 사용자 지정 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="24d43-103">Create a custom image from a VM</span></span>

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

## <a name="step-by-step-instructions"></a><span data-ttu-id="24d43-104">단계별 지침</span><span class="sxs-lookup"><span data-stu-id="24d43-104">Step-by-step instructions</span></span>

<span data-ttu-id="24d43-105">프로비저닝된 VM에서 사용자 지정 이미지를 만든 다음, 사용자 지정 이미지를 사용하여 동일한 VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24d43-105">You can create a custom image from a provisioned VM, and afterwards use that custom image to create identical VMs.</span></span> <span data-ttu-id="24d43-106">다음 단계에서는 VM에서 사용자 지정 이미지를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="24d43-106">The following steps illustrate how to create a custom image from a VM:</span></span>

1. <span data-ttu-id="24d43-107">[Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="24d43-107">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="24d43-108">**추가 서비스**를 선택한 후 목록에서 **DevTest Labs**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="24d43-108">Select **More services**, and then select **DevTest Labs** from the list.</span></span>

1. <span data-ttu-id="24d43-109">랩 목록에서 원하는 랩을 탭합니다.</span><span class="sxs-lookup"><span data-stu-id="24d43-109">From the list of labs, select the desired lab.</span></span>  

1. <span data-ttu-id="24d43-110">랩의 블레이드에서 **내 가상 컴퓨터**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="24d43-110">On the lab's blade, select **My virtual machines**.</span></span>
 
1. <span data-ttu-id="24d43-111">**내 가상 컴퓨터** 블레이드에서 사용자 지정 이미지를 만들 VM을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="24d43-111">On the **My virtual machines** blade, select the VM from which you want to create the custom image.</span></span>

1. <span data-ttu-id="24d43-112">VM의 블레이드에서 **사용자 지정 이미지 만들기(VHD)**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="24d43-112">On the VM's blade, select **Create custom image (VHD)**.</span></span>

    ![사용자 지정 이미지 만들기 메뉴 항목](./media/devtest-lab-create-template/create-custom-image.png)

1. <span data-ttu-id="24d43-114">**이미지 만들기** 블레이드에서 사용자 지정 이미지에 대한 이름 및 설명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="24d43-114">On the **Create image** blade, enter a name and description for your custom image.</span></span> <span data-ttu-id="24d43-115">이 정보는 VM을 만들 때 기본 목록에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="24d43-115">This information is displayed in the list of bases when you create a VM.</span></span>

    ![사용자 지정 이미지 만들기 블레이드](./media/devtest-lab-create-template/create-custom-image-blade.png)

1. <span data-ttu-id="24d43-117">sysprep이 VM에서 실행되었는지 여부를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="24d43-117">Select whether sysprep was run on the VM.</span></span> <span data-ttu-id="24d43-118">sysprep이 VM에서 실행되지 않은 경우 이 사용자 지정 이미지에서 VM을 만들 때 sysprep을 실행할지를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="24d43-118">If the sysprep was not run on the VM, specify whether you want sysprep run when a VM is created from this custom image.</span></span>

1. <span data-ttu-id="24d43-119">완료했으면 **확인** 을 선택하여 사용자 지정 이미지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="24d43-119">Select **OK** when finished to create the custom image.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="24d43-120">관련 블로그 게시물</span><span class="sxs-lookup"><span data-stu-id="24d43-120">Related blog posts</span></span>

- [<span data-ttu-id="24d43-121">사용자 지정 이미지 또는 수식?</span><span class="sxs-lookup"><span data-stu-id="24d43-121">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [<span data-ttu-id="24d43-122">Azure DevTest Labs 간의 사용자 지정 이미지 복사</span><span class="sxs-lookup"><span data-stu-id="24d43-122">Copying Custom Images between Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a><span data-ttu-id="24d43-123">다음 단계</span><span class="sxs-lookup"><span data-stu-id="24d43-123">Next steps</span></span>

- [<span data-ttu-id="24d43-124">랩에 VM 추가</span><span class="sxs-lookup"><span data-stu-id="24d43-124">Add a VM to your lab</span></span>](./devtest-lab-add-vm-with-artifacts.md)
