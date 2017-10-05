---
title: "학습에 Azure DevTest Labs 사용 | Microsoft 문서"
description: "학습 시나리오에 Azure DevTest Labs를 사용하는 방법을 알아봅니다."
services: devtest-lab,virtual-machines
documentationcenter: na
author: steved0x
manager: douge
editor: 
ms.assetid: 57ff4e30-7e33-453f-9867-e19b3fdb9fe2
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/12/2016
ms.author: sdanie
ms.openlocfilehash: a85999b7963e9a07d3f91ec47f298f91439c0808
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-devtest-labs-for-training"></a><span data-ttu-id="76c1c-103">학습에 Azure DevTest Labs 사용</span><span class="sxs-lookup"><span data-stu-id="76c1c-103">Use Azure DevTest Labs for training</span></span>
<span data-ttu-id="76c1c-104">Azure DevTest Labs는 개발/테스트 외에도 여러 주요 시나리오를 구현하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76c1c-104">Azure DevTest Labs can be used to implement many key scenarios in addition to dev/test.</span></span> <span data-ttu-id="76c1c-105">이러한 시나리오 중 하나는 학습용 랩을 설정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="76c1c-105">One of those scenarios is to set up a lab for training.</span></span> <span data-ttu-id="76c1c-106">Azure DevTest Labs를 통해 각 실습생이 동일하고 격리된 학습용 환경을 만드는 데 사용할 수 있는 사용자 지정 템플릿을 제공할 수 있는 랩을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76c1c-106">Azure DevTest Labs allows you to create a lab where you can provide custom templates that each trainee can use to create identical and isolated environments for training.</span></span> <span data-ttu-id="76c1c-107">각 실습생이 필요할 때에만 교육 환경을 이용할 수 있도록 하고 교육에 필요한 리소스(예: 가상 컴퓨터)를 충분히 포함하는 정책을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76c1c-107">You can apply policies to ensure that training environments are available to each trainee only when they need them and contain enough resources - such as virtual machines - required for the training.</span></span> <span data-ttu-id="76c1c-108">마지막으로 실습생과 랩을 쉽게 공유할 수 있고 실습생은 한 번의 클릭으로 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76c1c-108">Finally, you can easily share the lab with trainees, which they can access in one click.</span></span>

![학습에 DevTest Labs 사용](./media/devtest-lab-training-lab/devtest-lab-training.png)

<span data-ttu-id="76c1c-110">Azure DevTest Labs는 모든 가상 환경에서 학습을 수행하는 데 필요한 다음과 같은 요구 사항을 충족합니다.</span><span class="sxs-lookup"><span data-stu-id="76c1c-110">Azure DevTest Labs meets the following requirements that are required to conduct training in any virtual environment:</span></span> 

* <span data-ttu-id="76c1c-111">실습생은 다른 실습생이 만든 VM을 볼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="76c1c-111">Trainees cannot see VMs created by other trainees</span></span>
* <span data-ttu-id="76c1c-112">모든 학습 컴퓨터는 동일해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76c1c-112">Every training machine should be identical</span></span>
* <span data-ttu-id="76c1c-113">실습생은 학습 환경을 신속하게 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76c1c-113">Trainees can quickly provision their training environments</span></span>
* <span data-ttu-id="76c1c-114">실습생이 학습에 필요한 만큼의 VM만 사용하고 사용하지 않을 때는 VM을 종료하도록 하여 비용을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="76c1c-114">Control cost by ensuring that trainees cannot get more VMs than they need for the training and also shutdown VMs when they are not using them</span></span>
* <span data-ttu-id="76c1c-115">각 실습생과 학습 랩을 쉽게 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="76c1c-115">Easily share the training lab with each trainee</span></span>
* <span data-ttu-id="76c1c-116">학습 랩을 반복해서 다시 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="76c1c-116">Reuse the training lab again and again</span></span>

<span data-ttu-id="76c1c-117">이 문서에서는 앞에서 설명한 학습 요구 사항을 충족하는 데 사용할 수 있는 여러 Azure DevTest Labs 기능과 학습용 랩을 설정하는 데 수행할 수 있는 자세한 단계에 대해 학습합니다.</span><span class="sxs-lookup"><span data-stu-id="76c1c-117">In this article, you learn about various Azure DevTest Labs features that can be used to meet the previously described training requirements and detailed steps that you can follow to set up a lab for training.</span></span>  

## <a name="implementing-training-with-azure-devtest-labs"></a><span data-ttu-id="76c1c-118">Azure DevTest Labs로 학습 구현</span><span class="sxs-lookup"><span data-stu-id="76c1c-118">Implementing training with Azure DevTest Labs</span></span>
1. <span data-ttu-id="76c1c-119">**랩 만들기**</span><span class="sxs-lookup"><span data-stu-id="76c1c-119">**Create the lab**</span></span> 
   
    <span data-ttu-id="76c1c-120">랩은 Azure DevTest Labs의 시작 지점입니다.</span><span class="sxs-lookup"><span data-stu-id="76c1c-120">Labs are the starting point in Azure DevTest Labs.</span></span> <span data-ttu-id="76c1c-121">랩을 만든 후 랩에 사용자(실습생)를 추가하고, 비용을 제어하는 정책을 설정하고, 신속하게 만들 수 있는 VM 이미지를 정의하는 등의 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76c1c-121">Once you create a lab, you can perform tasks such as add users (trainees) to the lab, set policies to control costs, define VM images that can create quickly, and more.</span></span>   
   
    <span data-ttu-id="76c1c-122">다음 표에 있는 링크를 클릭하면 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76c1c-122">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="76c1c-123">작업</span><span class="sxs-lookup"><span data-stu-id="76c1c-123">Task</span></span> | <span data-ttu-id="76c1c-124">학습 내용</span><span class="sxs-lookup"><span data-stu-id="76c1c-124">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="76c1c-125">Azure DevTest Labs에서 랩 만들기</span><span class="sxs-lookup"><span data-stu-id="76c1c-125">Create a lab in Azure DevTest Labs</span></span>](devtest-lab-create-lab.md) |<span data-ttu-id="76c1c-126">Azure Portal의 Azure DevTest Labs에서 랩을 만드는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="76c1c-126">Learn how to create a lab in Azure DevTest Labs in the Azure portal.</span></span> |
2. <span data-ttu-id="76c1c-127">**바로 사용할 수 있는 마켓플레이스 이미지 및 사용자 지정 이미지를 사용하여 몇 분 만에 학습 VM 만들기**</span><span class="sxs-lookup"><span data-stu-id="76c1c-127">**Create training VMs in minutes using ready-made marketplace images and custom images**</span></span> 
   
    <span data-ttu-id="76c1c-128">Azure Marketplace의 다양한 이미지에서 바로 사용할 수 있는 이미지를 선택하고 랩의 실습생이 사용하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76c1c-128">You can pick ready-made images from a wide variety of images in the Azure Marketplace and make them available for the trainees in the lab.</span></span> <span data-ttu-id="76c1c-129">바로 사용할 수 있는 이미지가 요구 사항을 충족하지 않을 경우 Azure Marketplace에서 바로 사용할 수 있는 이미지를 사용하여 랩 VM을 만들고, 학습에 필요한 모든 소프트웨어를 설치하고, 랩의 사용자 지정 이미지로 VM을 지정함으로써 사용자 지정 이미지를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76c1c-129">If the ready-made images don't meet your requirements, you can create a custom image by creating a lab VM using a ready-made image from Azure Marketplace, installing all the software that you need for the training, and saving the VM as custom image in the lab.</span></span> 
   
    <span data-ttu-id="76c1c-130">다음 표에 있는 링크를 클릭하면 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76c1c-130">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="76c1c-131">작업</span><span class="sxs-lookup"><span data-stu-id="76c1c-131">Task</span></span> | <span data-ttu-id="76c1c-132">학습 내용</span><span class="sxs-lookup"><span data-stu-id="76c1c-132">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="76c1c-133">Azure Marketplace 이미지 구성</span><span class="sxs-lookup"><span data-stu-id="76c1c-133">Configure Azure Marketplace images</span></span>](devtest-lab-configure-marketplace-images.md) |<span data-ttu-id="76c1c-134">학습에 필요한 이미지만 선택할 수 있도록 Azure Marketplace 이미지를 허용 목록에 추가할 수 있는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="76c1c-134">Learn how you can whitelist Azure Marketplace images; making available for selection only the images you want for the training.</span></span> |
   | [<span data-ttu-id="76c1c-135">사용자 지정 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="76c1c-135">Create a custom image</span></span>](devtest-lab-create-template.md) |<span data-ttu-id="76c1c-136">실습생이 사용자 지정 이미지를 사용하여 신속하게 VM을 만들 수 있도록 학습에 필요한 소프트웨어를 미리 설치하여 사용자 지정 이미지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="76c1c-136">Create a custom image by pre-installing the software you need for the training so that trainees can quickly create a VM using the custom image.</span></span> |
3. <span data-ttu-id="76c1c-137">**학습용 컴퓨터에 대한 재사용 가능 템플릿 만들기**</span><span class="sxs-lookup"><span data-stu-id="76c1c-137">**Create reusable templates for training machines**</span></span> 
   
    <span data-ttu-id="76c1c-138">Azure DevTest Labs의 수식은 VM을 만드는 데 사용되는 기본 속성 값의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="76c1c-138">A formula in Azure DevTest Labs is a list of default property values used to create a VM.</span></span> <span data-ttu-id="76c1c-139">이미지, VM 크기(CPU와 RAM의 조합) 및 가상 네트워크를 선택하여 랩에서 수식을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76c1c-139">You can create a formula in the lab by picking an image, a VM size (a combination of CPU and RAM), and a virtual network.</span></span> <span data-ttu-id="76c1c-140">각 실습생은 랩에서 수식을 보고 수식을 사용하여 VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76c1c-140">Each trainee can see the formula in the lab and use it to create a VM.</span></span> 
   
    <span data-ttu-id="76c1c-141">다음 표에 있는 링크를 클릭하면 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76c1c-141">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="76c1c-142">작업</span><span class="sxs-lookup"><span data-stu-id="76c1c-142">Task</span></span> | <span data-ttu-id="76c1c-143">학습 내용</span><span class="sxs-lookup"><span data-stu-id="76c1c-143">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="76c1c-144">VM을 만드는 DevTest Labs 수식 관리</span><span class="sxs-lookup"><span data-stu-id="76c1c-144">Manage DevTest Labs formulas to create VMs</span></span>](devtest-lab-manage-formulas.md) |<span data-ttu-id="76c1c-145">이미지, VM 크기(CPU와 RAM의 조합) 및 가상 네트워크를 선택하여 수식을 만들 수 있는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="76c1c-145">Learn how you can create a formula by picking up an image, VM size (combination of CPU and RAM), and a virtual network.</span></span> |
4. <span data-ttu-id="76c1c-146">**비용 제어**</span><span class="sxs-lookup"><span data-stu-id="76c1c-146">**Control costs**</span></span>
   
    <span data-ttu-id="76c1c-147">Azure DevTest Labs를 통해 랩에서 실습생이 만들 수 있는 VM의 최대 수를 지정하는 정책을 랩에 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76c1c-147">Azure DevTest Labs allows you to set a policy in the lab to specify the maximum number of VMs that can be created by a trainee in the lab.</span></span> 
   
    <span data-ttu-id="76c1c-148">며칠 간 학습 시 하루 중 특정 시간에 모든 VM을 중지했다가 다음 날 자동으로 다시 시작하도록 하려면 랩에서 자동 종료 및 자동 시작 정책을 설정하여 쉽게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76c1c-148">If you are conducting multi-day training and want to stop all the VMs at a particular time of the day and then automatically restart them the following day, you can easily accomplish that by setting auto-shutdown and auto-start policies in the lab.</span></span> 
   
    <span data-ttu-id="76c1c-149">마지막으로 학습이 완료되면 단일 PowerShell 스크립트를 실행하여 모든 VM을 한 번에 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76c1c-149">Finally, when training is complete you can delete all the VMs at once by running a single PowerShell script.</span></span> 
   
    <span data-ttu-id="76c1c-150">다음 표에 있는 링크를 클릭하면 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76c1c-150">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="76c1c-151">작업</span><span class="sxs-lookup"><span data-stu-id="76c1c-151">Task</span></span> | <span data-ttu-id="76c1c-152">학습 내용</span><span class="sxs-lookup"><span data-stu-id="76c1c-152">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="76c1c-153">랩 정책 정의</span><span class="sxs-lookup"><span data-stu-id="76c1c-153">Define lab policies</span></span>](devtest-lab-set-lab-policy.md) |<span data-ttu-id="76c1c-154">랩에 정책을 설정하여 비용을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="76c1c-154">Control costs by setting policies in the lab.</span></span> |
   | [<span data-ttu-id="76c1c-155">PowerShell 스크립트를 사용하여 모든 랩 VM 삭제</span><span class="sxs-lookup"><span data-stu-id="76c1c-155">Delete all the lab VMs using a PowerShell script</span></span>](devtest-lab-faq.md#how-can-i-automate-the-process-of-deleting-all-the-vms-in-my-lab) |<span data-ttu-id="76c1c-156">학습이 완료되면 한 번에 모든 랩을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="76c1c-156">Delete all the labs in one operation when the training is complete.</span></span> |
5. <span data-ttu-id="76c1c-157">**각 실습생과 랩 공유**</span><span class="sxs-lookup"><span data-stu-id="76c1c-157">**Share the lab with each trainee**</span></span>
   
    <span data-ttu-id="76c1c-158">실습생과 공유하는 링크를 사용하여 랩에 직접 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76c1c-158">Labs can be directly accessed using a link that you share with your trainees.</span></span> <span data-ttu-id="76c1c-159">[Microsoft 계정](devtest-lab-faq.md#what-is-a-microsoft-account)이 있는 실습생은 Azure 계정이 없어도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="76c1c-159">Your trainees don't even have to have an Azure account, as long as they have a [Microsoft account](devtest-lab-faq.md#what-is-a-microsoft-account).</span></span> <span data-ttu-id="76c1c-160">실습생은 다른 실습생이 만든 VM을 볼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="76c1c-160">Trainees cannot see VMs created by other trainees.</span></span>  
   
    <span data-ttu-id="76c1c-161">다음 표에 있는 링크를 클릭하면 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76c1c-161">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="76c1c-162">작업</span><span class="sxs-lookup"><span data-stu-id="76c1c-162">Task</span></span> | <span data-ttu-id="76c1c-163">학습 내용</span><span class="sxs-lookup"><span data-stu-id="76c1c-163">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="76c1c-164">Azure DevTest Labs에서 랩에 실습생 추가</span><span class="sxs-lookup"><span data-stu-id="76c1c-164">Add a trainee to a lab in Azure DevTest Labs</span></span>](devtest-lab-add-devtest-user.md) |<span data-ttu-id="76c1c-165">Azure Portal을 사용하여 학습 랩에 실습생을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="76c1c-165">Use the Azure portal to add trainees to your training lab.</span></span> |
   | [<span data-ttu-id="76c1c-166">PowerShell 스크립트를 사용하여 랩에 실습생 추가</span><span class="sxs-lookup"><span data-stu-id="76c1c-166">Add trainees to the lab using a PowerShell script</span></span>](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell) |<span data-ttu-id="76c1c-167">PowerShell을 사용하여 학습 랩에 자동으로 실습생을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="76c1c-167">Use PowerShell to automate adding trainees to your training lab.</span></span> |
   | [<span data-ttu-id="76c1c-168">랩에 대한 링크 가져오기</span><span class="sxs-lookup"><span data-stu-id="76c1c-168">Get a link to the lab</span></span>](devtest-lab-faq.md#how-do-i-share-a-direct-link-to-my-lab) |<span data-ttu-id="76c1c-169">하이퍼링크를 통해 랩에 바로 액세스할 수 있는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="76c1c-169">Learn how a lab can be directly accessed via a hyperlink.</span></span> |
6. <span data-ttu-id="76c1c-170">**랩을 반복해서 다시 사용**</span><span class="sxs-lookup"><span data-stu-id="76c1c-170">**Reuse the lab again and again**</span></span> 
   
    <span data-ttu-id="76c1c-171">Resource Manager 템플릿을 만들어 동일한 랩을 반복해서 다시 만드는 데 사용하면 사용자 지정 설정을 포함하여 랩 만들기를 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76c1c-171">You can automate lab creation, including custom settings, by creating a Resource Manager template and using it to create identical labs again and again.</span></span> 
   
    <span data-ttu-id="76c1c-172">다음 표에 있는 링크를 클릭하면 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76c1c-172">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="76c1c-173">작업</span><span class="sxs-lookup"><span data-stu-id="76c1c-173">Task</span></span> | <span data-ttu-id="76c1c-174">학습 내용</span><span class="sxs-lookup"><span data-stu-id="76c1c-174">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="76c1c-175">Resource Manager 템플릿을 사용하여 랩 만들기</span><span class="sxs-lookup"><span data-stu-id="76c1c-175">Create a lab using a Resource Manager template</span></span>](devtest-lab-faq.md#how-do-i-create-a-lab-from-an-azure-resource-manager-template) |<span data-ttu-id="76c1c-176">Resource Manager 템플릿을 사용하여 Azure DevTest Labs에서 랩을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="76c1c-176">Create labs in Azure DevTest Labs using Resource Manager templates.</span></span> |

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

