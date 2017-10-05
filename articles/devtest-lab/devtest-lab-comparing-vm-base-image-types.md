---
title: "DevTest Labs에서 사용자 지정 이미지와 수식 비교 | Microsoft 문서"
description: "사용자 환경에 가장 적합한 것이 무엇인지 결정할 수 있도록, VM 기반으로서 사용자 지정 이미지와 수식 사이의 차이점에 대해 알아봅니다."
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
ms.openlocfilehash: ff771abc26c08f0adb977c29739d2f5c91924b21
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="comparing-custom-images-and-formulas-in-devtest-labs"></a><span data-ttu-id="60f05-103">DevTest Lab에서 사용자 지정 이미지와 수식 비교</span><span class="sxs-lookup"><span data-stu-id="60f05-103">Comparing custom images and formulas in DevTest Labs</span></span>
<span data-ttu-id="60f05-104">[사용자 지정 이미지](devtest-lab-create-template.md) 및 [수식](devtest-lab-manage-formulas.md)은 모두 [새로 생성된 VM](devtest-lab-add-vm-with-artifacts.md)의 기반으로 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60f05-104">Both [custom images](devtest-lab-create-template.md) and [formulas](devtest-lab-manage-formulas.md) can be used as bases for [created new VMs](devtest-lab-add-vm-with-artifacts.md).</span></span> <span data-ttu-id="60f05-105">하지만 사용자 지정 이미지와 수식의 주요 차이점은 사용자 지정 이미지는 단지 VHD에 기반하는 이미지인 반면, 수식은 VHD *뿐만 아니라* 미리 구성된 설정(예: VM 크기, 가상 네트워크, 서브넷 및 아티팩트)에 기반하는 이미지라는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="60f05-105">However, the key distinction between custom images and formulas is that a custom image is simply an image based on a VHD, while a formula is an image based on a VHD *in addition to* preconfigured settings - such as VM Size, virtual network, subnet, and artifacts.</span></span> <span data-ttu-id="60f05-106">미리 구성된 설정은 VM을 만들 때 재정의될 수 있는 기본 값으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="60f05-106">These preconfigured settings are set up with default values that can be overridden at the time of VM creation.</span></span> <span data-ttu-id="60f05-107">이 문서는 사용자 지정 이미지 사용 대비 수식 사용의 장점과 단점을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="60f05-107">This article explains some of the advantages (pros) and disadvantages (cons) to using custom images versus using formulas.</span></span>

## <a name="custom-image-pros-and-cons"></a><span data-ttu-id="60f05-108">사용자 지정 이미지의 장점 및 단점</span><span class="sxs-lookup"><span data-stu-id="60f05-108">Custom image pros and cons</span></span>
<span data-ttu-id="60f05-109">사용자 지정 이미지는 원하는 환경에서 VM을 만드는 정적이고 변경할 수 없는 방식을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="60f05-109">Custom images provide a static, immutable way to create VMs from a desired environment.</span></span> 

<span data-ttu-id="60f05-110">**장점**</span><span class="sxs-lookup"><span data-stu-id="60f05-110">**Pros**</span></span>

* <span data-ttu-id="60f05-111">사용자 지정 이미지를 통한 VM 프로비전은 이미지를 통해 VM이 작동된 후에 변하는 것이 없을 정도로 빠릅니다.</span><span class="sxs-lookup"><span data-stu-id="60f05-111">VM provisioning from a custom image is fast as nothing changes after the VM is spun up from the image.</span></span> <span data-ttu-id="60f05-112">즉, 사용자 지정 이미지는 설정이 없는 단순한 이미지이기 때문에 적용할 설정이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="60f05-112">In other words, there are no settings to apply as the custom image is just an image without settings.</span></span> 
* <span data-ttu-id="60f05-113">하나의 사용자 지정 이미지를 통해 만들어진 VM은 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="60f05-113">VMs created from a single custom image are identical.</span></span>

<span data-ttu-id="60f05-114">**단점**</span><span class="sxs-lookup"><span data-stu-id="60f05-114">**Cons**</span></span>

* <span data-ttu-id="60f05-115">사용자 지정 이미지의 일부를 업데이트해야 하는 경우에는 이미지를 다시 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60f05-115">If you need to update some aspect of the custom image, the image must be recreated.</span></span>  

## <a name="formula-pros-and-cons"></a><span data-ttu-id="60f05-116">수식의 장점 및 단점</span><span class="sxs-lookup"><span data-stu-id="60f05-116">Formula pros and cons</span></span>
<span data-ttu-id="60f05-117">수식은 원하는 구성/설정을 통해 VM을 만드는 동적인 방식을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="60f05-117">Formulas provide a dynamic way to create VMs from the desired configuration/settings.</span></span>

<span data-ttu-id="60f05-118">**장점**</span><span class="sxs-lookup"><span data-stu-id="60f05-118">**Pros**</span></span>

* <span data-ttu-id="60f05-119">환경이 변하면 아티팩트를 통해 즉시 캡처할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60f05-119">Changes in the environment can be captured on the fly via artifacts.</span></span> <span data-ttu-id="60f05-120">예를 들어, 릴리스 파이프라인의 최신 비트를 사용하여 VM을 설치하거나 리포지토리의 최신 코드를 요청하려면, 대상 기본 이미지와 함께, 수식에 포함된 최신 비트를 배포하거나 최신 코드를 등록하는 아티팩트만 지정하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="60f05-120">For example, if you want a VM installed with the latest bits from your release pipeline or enlist the latest code from your repository, you can simply specify an artifact that deploys the latest bits or enlists the latest code in the formula together with a target base image.</span></span> <span data-ttu-id="60f05-121">수식을 사용하여 VM을 만들 때 마다, 최신 비트/코드가 VM에 배포/등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="60f05-121">Whenever this formula is used to create VMs, the latest bits/code are deployed/enlisted to the VM.</span></span> 
* <span data-ttu-id="60f05-122">수식은 사용자 지정 이미지가 제공할 수 없는 기본 설정(예: VM 크기 및 가상 네트워크 설정)을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60f05-122">Formulas can define default settings that custom images cannot provide - such as VM sizes and virtual network settings.</span></span> 
* <span data-ttu-id="60f05-123">수식에 저장된 설정은 기본 값으로 표시되지만 VM을 만들 때 수정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60f05-123">The settings saved in a formula are shown as default values, but can be modified when the VM is created.</span></span> 

<span data-ttu-id="60f05-124">**단점**</span><span class="sxs-lookup"><span data-stu-id="60f05-124">**Cons**</span></span>

* <span data-ttu-id="60f05-125">수식을 통해 VM을 만들면 사용자 지정 이미지를 통해 VM을 만드는 것보다 시간이 더 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="60f05-125">Creating a VM from a formula can take more time than creating a VM from a custom image.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="60f05-126">관련 블로그 게시물</span><span class="sxs-lookup"><span data-stu-id="60f05-126">Related blog posts</span></span>
* [<span data-ttu-id="60f05-127">사용자 지정 이미지 또는 수식?</span><span class="sxs-lookup"><span data-stu-id="60f05-127">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)

## <a name="next-steps"></a><span data-ttu-id="60f05-128">다음 단계</span><span class="sxs-lookup"><span data-stu-id="60f05-128">Next steps</span></span>
- [<span data-ttu-id="60f05-129">DevTest Labs FAQ</span><span class="sxs-lookup"><span data-stu-id="60f05-129">DevTest Labs FAQ</span></span>](devtest-lab-faq.md)