---
title: "aaaComparing 사용자 지정 이미지 및 수식에서 DevTest Labs | Microsoft Docs"
description: "VM 기반 환경에 가장 적합 한 어떤 것을 결정할 수 있도록 사용자 지정 이미지와 수식 hello 차이점에 알아봅니다."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: a3cb259a-7d80-40ec-8ee8-45105704d589
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: tarcher
ms.openlocfilehash: 3c1d88dfe0ff94b8e825bb7a0b4aca3341c9330d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="comparing-custom-images-and-formulas-in-devtest-labs"></a><span data-ttu-id="2878e-103">DevTest Lab에서 사용자 지정 이미지와 수식 비교</span><span class="sxs-lookup"><span data-stu-id="2878e-103">Comparing custom images and formulas in DevTest Labs</span></span>
<span data-ttu-id="2878e-104">[사용자 지정 이미지](devtest-lab-create-template.md) 및 [수식](devtest-lab-manage-formulas.md)은 모두 [새로 생성된 VM](devtest-lab-add-vm-with-artifacts.md)의 기반으로 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2878e-104">Both [custom images](devtest-lab-create-template.md) and [formulas](devtest-lab-manage-formulas.md) can be used as bases for [created new VMs](devtest-lab-add-vm-with-artifacts.md).</span></span> <span data-ttu-id="2878e-105">그러나 hello 중요 한 차이점 수식와 사용자 지정 이미지 간의 사용자 지정 이미지 수식은 VHD를 기반으로 이미지는 VHD를 기반으로 이미지 단순히 된다는 점입니다 *외에* 설정-VM 크기, 가상 네트워크와 같은 미리 구성 서브넷 및 아티팩트를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2878e-105">However, hello key distinction between custom images and formulas is that a custom image is simply an image based on a VHD, while a formula is an image based on a VHD *in addition to* preconfigured settings - such as VM Size, virtual network, subnet, and artifacts.</span></span> <span data-ttu-id="2878e-106">미리 구성 된 이러한 설정은 hello VM 생성 시 재정의할 수 있는 기본 값으로 설정 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2878e-106">These preconfigured settings are set up with default values that can be overridden at hello time of VM creation.</span></span> <span data-ttu-id="2878e-107">이 문서 (전문가) hello 장점 중 일부에 대해 설명 하 고 (cons) 및 수식을 사용 하 여 사용자 지정 이미지 toousing 단점입니다.</span><span class="sxs-lookup"><span data-stu-id="2878e-107">This article explains some of hello advantages (pros) and disadvantages (cons) toousing custom images versus using formulas.</span></span>

## <a name="custom-image-pros-and-cons"></a><span data-ttu-id="2878e-108">사용자 지정 이미지의 장점 및 단점</span><span class="sxs-lookup"><span data-stu-id="2878e-108">Custom image pros and cons</span></span>
<span data-ttu-id="2878e-109">사용자 지정 이미지 정적, 변경할 수 없는 방식으로 toocreate Vm 원하는 환경에서 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2878e-109">Custom images provide a static, immutable way toocreate VMs from a desired environment.</span></span> 

<span data-ttu-id="2878e-110">**장점**</span><span class="sxs-lookup"><span data-stu-id="2878e-110">**Pros**</span></span>

* <span data-ttu-id="2878e-111">VM 사용자 지정 이미지에서 프로 비전 hello 이미지에서 VM을 된 hello 후 변경 사항이 없는 빠릅니다.</span><span class="sxs-lookup"><span data-stu-id="2878e-111">VM provisioning from a custom image is fast as nothing changes after hello VM is spun up from hello image.</span></span> <span data-ttu-id="2878e-112">즉, 없음 설정을 tooapply hello 사용자 지정 이미지는이 설정이 없는 이미지로 합니다.</span><span class="sxs-lookup"><span data-stu-id="2878e-112">In other words, there are no settings tooapply as hello custom image is just an image without settings.</span></span> 
* <span data-ttu-id="2878e-113">하나의 사용자 지정 이미지를 통해 만들어진 VM은 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="2878e-113">VMs created from a single custom image are identical.</span></span>

<span data-ttu-id="2878e-114">**단점**</span><span class="sxs-lookup"><span data-stu-id="2878e-114">**Cons**</span></span>

* <span data-ttu-id="2878e-115">Hello 사용자 지정 이미지의 일부 측면 tooupdate 해야 할 경우 hello 이미지를 다시 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2878e-115">If you need tooupdate some aspect of hello custom image, hello image must be recreated.</span></span>  

## <a name="formula-pros-and-cons"></a><span data-ttu-id="2878e-116">수식의 장점 및 단점</span><span class="sxs-lookup"><span data-stu-id="2878e-116">Formula pros and cons</span></span>
<span data-ttu-id="2878e-117">수식은 동적 방법으로 toocreate Vm에서 필요한 hello 구성/설정을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2878e-117">Formulas provide a dynamic way toocreate VMs from hello desired configuration/settings.</span></span>

<span data-ttu-id="2878e-118">**장점**</span><span class="sxs-lookup"><span data-stu-id="2878e-118">**Pros**</span></span>

* <span data-ttu-id="2878e-119">아티팩트를 통해 신속 하 게 hello hello 환경에서 변경 내용은 캡처할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2878e-119">Changes in hello environment can be captured on hello fly via artifacts.</span></span> <span data-ttu-id="2878e-120">예를 들어, 릴리스 파이프라인에서 최신 파일 hello와 함께 설치 된 VM 이나 hello 최신 코드 리포지토리에서 참여를 지정할 수 있습니다 단순히 hello와 함께 hello 수식에 최신 코드를 인 리스트 먼 트 또는 hello 최신 파일을 배포 하는 아티팩트는 대상 기본 이미지입니다.</span><span class="sxs-lookup"><span data-stu-id="2878e-120">For example, if you want a VM installed with hello latest bits from your release pipeline or enlist hello latest code from your repository, you can simply specify an artifact that deploys hello latest bits or enlists hello latest code in hello formula together with a target base image.</span></span> <span data-ttu-id="2878e-121">이 수식을 사용 하는 toocreate Vm 때마다 hello 최신 비트/코드 배포/참여 toohello VM는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2878e-121">Whenever this formula is used toocreate VMs, hello latest bits/code are deployed/enlisted toohello VM.</span></span> 
* <span data-ttu-id="2878e-122">수식은 사용자 지정 이미지가 제공할 수 없는 기본 설정(예: VM 크기 및 가상 네트워크 설정)을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2878e-122">Formulas can define default settings that custom images cannot provide - such as VM sizes and virtual network settings.</span></span> 
* <span data-ttu-id="2878e-123">수식에 저장 된 hello 설정은 기본 값으로 표시 되지만 VM hello를 만들 때에 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2878e-123">hello settings saved in a formula are shown as default values, but can be modified when hello VM is created.</span></span> 

<span data-ttu-id="2878e-124">**단점**</span><span class="sxs-lookup"><span data-stu-id="2878e-124">**Cons**</span></span>

* <span data-ttu-id="2878e-125">수식을 통해 VM을 만들면 사용자 지정 이미지를 통해 VM을 만드는 것보다 시간이 더 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="2878e-125">Creating a VM from a formula can take more time than creating a VM from a custom image.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="2878e-126">관련 블로그 게시물</span><span class="sxs-lookup"><span data-stu-id="2878e-126">Related blog posts</span></span>
* [<span data-ttu-id="2878e-127">사용자 지정 이미지 또는 수식?</span><span class="sxs-lookup"><span data-stu-id="2878e-127">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)

## <a name="next-steps"></a><span data-ttu-id="2878e-128">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2878e-128">Next steps</span></span>
- [<span data-ttu-id="2878e-129">DevTest Labs FAQ</span><span class="sxs-lookup"><span data-stu-id="2878e-129">DevTest Labs FAQ</span></span>](devtest-lab-faq.md)