---
title: "VHD 파일의 사용자 지정 이미지를 Azure DevTest Labs aaaCreate | Microsoft Docs"
description: "Toocreate Azure DevTest Labs에는 사용자 지정 이미지를 사용 하 여 VHD 파일에서 Azure 포털을 hello 하는 방법에 대해 알아봅니다"
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
ms.openlocfilehash: 80af8ea1cb72380f868df0a76c4a0dcd92e63cf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-from-a-vhd-file"></a><span data-ttu-id="31802-103">VHD 파일에서 사용자 지정 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="31802-103">Create a custom image from a VHD file</span></span>

[!INCLUDE [devtest-lab-create-custom-image-from-vhd-selector](../../includes/devtest-lab-create-custom-image-from-vhd-selector.md)]

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

[!INCLUDE [devtest-lab-upload-vhd-options](../../includes/devtest-lab-upload-vhd-options.md)]

## <a name="step-by-step-instructions"></a><span data-ttu-id="31802-104">단계별 지침</span><span class="sxs-lookup"><span data-stu-id="31802-104">Step-by-step instructions</span></span>

<span data-ttu-id="31802-105">hello 다음 단계를 안내 hello Azure 포털을 사용 하 여 VHD 파일에서 사용자 지정 이미지 만들기:</span><span class="sxs-lookup"><span data-stu-id="31802-105">hello following steps walk you through creating a custom image from a VHD file using hello Azure portal:</span></span>

1. <span data-ttu-id="31802-106">Toohello 로그인 [Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)합니다.</span><span class="sxs-lookup"><span data-stu-id="31802-106">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="31802-107">선택 **더 많은 서비스**를 선택한 후 **DevTest Labs** hello 목록에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="31802-107">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>

1. <span data-ttu-id="31802-108">랩의 hello 목록에서 원하는 랩 hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="31802-108">From hello list of labs, select hello desired lab.</span></span>  

1. <span data-ttu-id="31802-109">Hello 랩 블레이드에서 선택 **구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="31802-109">On hello lab's blade, select **Configuration**.</span></span> 

1. <span data-ttu-id="31802-110">Hello 랩에 **구성** 블레이드를 **사용자 지정 이미지 (Vhd)**합니다.</span><span class="sxs-lookup"><span data-stu-id="31802-110">On hello lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>

1. <span data-ttu-id="31802-111">Hello에 **사용자 지정 이미지** 블레이드를 **+ 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="31802-111">On hello **Custom images** blade, select **+Add**.</span></span>

    ![사용자 지정 이미지 추가](./media/devtest-lab-create-template/add-custom-image.png)

1. <span data-ttu-id="31802-113">Hello hello 사용자 지정 이미지 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="31802-113">Enter hello name of hello custom image.</span></span> <span data-ttu-id="31802-114">이 이름은 VM을 만들 때 기본 이미지의 hello 목록에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="31802-114">This name is displayed in hello list of base images when creating a VM.</span></span>

1. <span data-ttu-id="31802-115">Hello hello 사용자 지정 이미지에 대 한 설명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="31802-115">Enter hello description of hello custom image.</span></span> <span data-ttu-id="31802-116">이 설명은 VM을 만들 때 기본 이미지의 hello 목록에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="31802-116">This description is displayed in hello list of base images when creating a VM.</span></span>

1. <span data-ttu-id="31802-117">**VHD**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="31802-117">Select **VHD**.</span></span>

1. <span data-ttu-id="31802-118">Hello에서 **VHD** 블레이드, 원하는 선택 hello VHD 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="31802-118">From hello **VHD** blade, select hello desired VHD file.</span></span>

1. <span data-ttu-id="31802-119">선택 **확인** tooclose hello **VHD** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="31802-119">Select **OK** tooclose hello **VHD** blade.</span></span>

1. <span data-ttu-id="31802-120">**OS 구성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="31802-120">Select **OS configuration**.</span></span>

1. <span data-ttu-id="31802-121">Hello에 **운영 체제 구성** 탭을 선택 하거나 **Windows** 또는 **Linux**합니다.</span><span class="sxs-lookup"><span data-stu-id="31802-121">On hello **OS configuration** tab, select either **Windows** or **Linux**.</span></span>

1. <span data-ttu-id="31802-122">경우 **Windows** 은 선택한 경우 hello 확인란을 통해 지정 여부 *Sysprep* hello 컴퓨터에서 실행 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="31802-122">If **Windows** is selected, specify via hello checkbox whether *Sysprep* has been run on hello machine.</span></span> 

1. <span data-ttu-id="31802-123">선택 **확인** tooclose hello **운영 체제 구성** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="31802-123">Select **OK** tooclose hello **OS configuration** blade.</span></span>

1. <span data-ttu-id="31802-124">선택 **확인** toocreate hello에 대 한 사용자 지정 이미지입니다.</span><span class="sxs-lookup"><span data-stu-id="31802-124">Select **OK** toocreate hello custom image.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="31802-125">관련 블로그 게시물</span><span class="sxs-lookup"><span data-stu-id="31802-125">Related blog posts</span></span>

- [<span data-ttu-id="31802-126">사용자 지정 이미지 또는 수식?</span><span class="sxs-lookup"><span data-stu-id="31802-126">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [<span data-ttu-id="31802-127">Azure DevTest Labs 간의 사용자 지정 이미지 복사</span><span class="sxs-lookup"><span data-stu-id="31802-127">Copying Custom Images between Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a><span data-ttu-id="31802-128">다음 단계</span><span class="sxs-lookup"><span data-stu-id="31802-128">Next steps</span></span>

- [<span data-ttu-id="31802-129">추가 VM tooyour 랩</span><span class="sxs-lookup"><span data-stu-id="31802-129">Add a VM tooyour lab</span></span>](./devtest-lab-add-vm-with-artifacts.md)
