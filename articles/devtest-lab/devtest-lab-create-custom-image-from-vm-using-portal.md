---
title: "VM의 사용자 지정 이미지를 Azure DevTest Labs aaaCreate | Microsoft Docs"
description: "Toocreate Azure DevTest Labs에는 사용자 지정 이미지를 사용 하 여 프로 비전 된 VM에서 Azure 포털을 hello 하는 방법에 대해 알아봅니다"
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
ms.openlocfilehash: 7dccb79d3db4aae676c7bd2f6b800301210491e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-from-a-vm"></a><span data-ttu-id="e281a-103">VM에서 사용자 지정 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="e281a-103">Create a custom image from a VM</span></span>

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

## <a name="step-by-step-instructions"></a><span data-ttu-id="e281a-104">단계별 지침</span><span class="sxs-lookup"><span data-stu-id="e281a-104">Step-by-step instructions</span></span>

<span data-ttu-id="e281a-105">프로 비전 된 VM에서 사용자 지정 이미지를 만들 하 고 나중에 해당 사용자 지정 이미지 toocreate를 사용 하 여 동일한 Vm입니다.</span><span class="sxs-lookup"><span data-stu-id="e281a-105">You can create a custom image from a provisioned VM, and afterwards use that custom image toocreate identical VMs.</span></span> <span data-ttu-id="e281a-106">단계를 수행 하는 hello 방법을 toocreate 사용자 지정은 VM에서을 이미지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e281a-106">hello following steps illustrate how toocreate a custom image from a VM:</span></span>

1. <span data-ttu-id="e281a-107">Toohello 로그인 [Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)합니다.</span><span class="sxs-lookup"><span data-stu-id="e281a-107">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="e281a-108">선택 **더 많은 서비스**를 선택한 후 **DevTest Labs** hello 목록에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="e281a-108">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>

1. <span data-ttu-id="e281a-109">랩의 hello 목록에서 원하는 랩 hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e281a-109">From hello list of labs, select hello desired lab.</span></span>  

1. <span data-ttu-id="e281a-110">Hello 랩 블레이드에서 선택 **내 가상 컴퓨터**합니다.</span><span class="sxs-lookup"><span data-stu-id="e281a-110">On hello lab's blade, select **My virtual machines**.</span></span>
 
1. <span data-ttu-id="e281a-111">Hello에 **내 가상 컴퓨터** 블레이드에서 toocreate hello에 대 한 사용자 지정 이미지를 제거할 선택 hello VM입니다.</span><span class="sxs-lookup"><span data-stu-id="e281a-111">On hello **My virtual machines** blade, select hello VM from which you want toocreate hello custom image.</span></span>

1. <span data-ttu-id="e281a-112">Hello VM 블레이드에서 선택 **사용자 지정 이미지 만들기 (VHD)**합니다.</span><span class="sxs-lookup"><span data-stu-id="e281a-112">On hello VM's blade, select **Create custom image (VHD)**.</span></span>

    ![사용자 지정 이미지 만들기 메뉴 항목](./media/devtest-lab-create-template/create-custom-image.png)

1. <span data-ttu-id="e281a-114">Hello에 **이미지 만들기** 블레이드에서 이름 및 사용자 지정 이미지에 대 한 설명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e281a-114">On hello **Create image** blade, enter a name and description for your custom image.</span></span> <span data-ttu-id="e281a-115">이 정보는 VM을 만들 때 기본 hello 목록에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e281a-115">This information is displayed in hello list of bases when you create a VM.</span></span>

    ![사용자 지정 이미지 만들기 블레이드](./media/devtest-lab-create-template/create-custom-image-blade.png)

1. <span data-ttu-id="e281a-117">Sysprep가 hello VM에서 실행 하는지 여부를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e281a-117">Select whether sysprep was run on hello VM.</span></span> <span data-ttu-id="e281a-118">Hello sysprep hello VM에서 실행 되지 않았습니다, VM이 사용자 지정 이미지에서 생성 될 때 실행 하는 sysprep 사용할지를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e281a-118">If hello sysprep was not run on hello VM, specify whether you want sysprep run when a VM is created from this custom image.</span></span>

1. <span data-ttu-id="e281a-119">선택 **확인** 완료 toocreate 사용자 지정 이미지를 hello 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="e281a-119">Select **OK** when finished toocreate hello custom image.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="e281a-120">관련 블로그 게시물</span><span class="sxs-lookup"><span data-stu-id="e281a-120">Related blog posts</span></span>

- [<span data-ttu-id="e281a-121">사용자 지정 이미지 또는 수식?</span><span class="sxs-lookup"><span data-stu-id="e281a-121">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [<span data-ttu-id="e281a-122">Azure DevTest Labs 간의 사용자 지정 이미지 복사</span><span class="sxs-lookup"><span data-stu-id="e281a-122">Copying Custom Images between Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a><span data-ttu-id="e281a-123">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e281a-123">Next steps</span></span>

- [<span data-ttu-id="e281a-124">추가 VM tooyour 랩</span><span class="sxs-lookup"><span data-stu-id="e281a-124">Add a VM tooyour lab</span></span>](./devtest-lab-add-vm-with-artifacts.md)
