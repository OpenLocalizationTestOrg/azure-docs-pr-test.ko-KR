---
title: "학습에 대 한 Azure DevTest Labs aaaUse | Microsoft Docs"
description: "자세한 내용은 방법 교육 시나리오에 대 한 Azure DevTest Labs toouse 합니다."
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
ms.openlocfilehash: 4a5f44a282d8f6a58849c730ff89237ccff39ca8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-devtest-labs-for-training"></a><span data-ttu-id="d85c4-103">학습에 Azure DevTest Labs 사용</span><span class="sxs-lookup"><span data-stu-id="d85c4-103">Use Azure DevTest Labs for training</span></span>
<span data-ttu-id="d85c4-104">Azure DevTest Labs 사용된 tooimplement 더하기 toodev/테스트에 여러 주요 시나리오 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d85c4-104">Azure DevTest Labs can be used tooimplement many key scenarios in addition toodev/test.</span></span> <span data-ttu-id="d85c4-105">이러한 시나리오 중 하나는 학습에 랩을 tooset 합니다.</span><span class="sxs-lookup"><span data-stu-id="d85c4-105">One of those scenarios is tooset up a lab for training.</span></span> <span data-ttu-id="d85c4-106">Azure DevTest Labs 사용 하면 사용자 지정 서식 파일을 제공할 수 있는 랩 toocreate 각 학습자를 학습에 toocreate 동일 하 고 격리 된 환경을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d85c4-106">Azure DevTest Labs allows you toocreate a lab where you can provide custom templates that each trainee can use toocreate identical and isolated environments for training.</span></span> <span data-ttu-id="d85c4-107">정책을 tooensure 학습 환경은 사용할 수 있는 tooeach 학습자 필요 하며 충분 한 리소스-hello 학습에 필요한 가상 컴퓨터-예: 포함 하는 경우에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d85c4-107">You can apply policies tooensure that training environments are available tooeach trainee only when they need them and contain enough resources - such as virtual machines - required for hello training.</span></span> <span data-ttu-id="d85c4-108">마지막으로, 한 번의 클릭에서 액세스할 수 있는 교육와 hello 랩 쉽게 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d85c4-108">Finally, you can easily share hello lab with trainees, which they can access in one click.</span></span>

![학습에 DevTest Labs 사용](./media/devtest-lab-training-lab/devtest-lab-training.png)

<span data-ttu-id="d85c4-110">Azure DevTest Labs 가상 환경에서 필요한 tooconduct 학습 된 요구 사항을 준수 하는 hello를 충족 합니다.</span><span class="sxs-lookup"><span data-stu-id="d85c4-110">Azure DevTest Labs meets hello following requirements that are required tooconduct training in any virtual environment:</span></span> 

* <span data-ttu-id="d85c4-111">실습생은 다른 실습생이 만든 VM을 볼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d85c4-111">Trainees cannot see VMs created by other trainees</span></span>
* <span data-ttu-id="d85c4-112">모든 학습 컴퓨터는 동일해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d85c4-112">Every training machine should be identical</span></span>
* <span data-ttu-id="d85c4-113">실습생은 학습 환경을 신속하게 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d85c4-113">Trainees can quickly provision their training environments</span></span>
* <span data-ttu-id="d85c4-114">교육을 사용 하지 않는 경우 hello 교육 및 Vm 종료에 대 한 필요한 보다 더 많은 Vm을 가져올 수 없습니다 되도록 하 여 비용을 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="d85c4-114">Control cost by ensuring that trainees cannot get more VMs than they need for hello training and also shutdown VMs when they are not using them</span></span>
* <span data-ttu-id="d85c4-115">Hello 교육 랩 각 학습자와 쉽게 공유할 수</span><span class="sxs-lookup"><span data-stu-id="d85c4-115">Easily share hello training lab with each trainee</span></span>
* <span data-ttu-id="d85c4-116">나중에 다시 교육 랩 hello를 다시 사용</span><span class="sxs-lookup"><span data-stu-id="d85c4-116">Reuse hello training lab again and again</span></span>

<span data-ttu-id="d85c4-117">이 문서에서는 배웁니다 사용할 수 있는 다양 한 Azure DevTest Labs 기능에 대 한 toomeet hello 앞에서 설명한 교육 요구 사항 및 단계 학습을 위해 랩을 tooset를 따를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d85c4-117">In this article, you learn about various Azure DevTest Labs features that can be used toomeet hello previously described training requirements and detailed steps that you can follow tooset up a lab for training.</span></span>  

## <a name="implementing-training-with-azure-devtest-labs"></a><span data-ttu-id="d85c4-118">Azure DevTest Labs로 학습 구현</span><span class="sxs-lookup"><span data-stu-id="d85c4-118">Implementing training with Azure DevTest Labs</span></span>
1. <span data-ttu-id="d85c4-119">**Hello 랩 만들기**</span><span class="sxs-lookup"><span data-stu-id="d85c4-119">**Create hello lab**</span></span> 
   
    <span data-ttu-id="d85c4-120">랩은 hello Azure DevTest Labs의 시작 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="d85c4-120">Labs are hello starting point in Azure DevTest Labs.</span></span> <span data-ttu-id="d85c4-121">랩을 만든 후 같은 추가 사용자 (교육) toohello 랩 정책 toocontrol 비용을 설정 하 고, 정의 VM 이미지를 신속 하 게 만들 수 있는 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d85c4-121">Once you create a lab, you can perform tasks such as add users (trainees) toohello lab, set policies toocontrol costs, define VM images that can create quickly, and more.</span></span>   
   
    <span data-ttu-id="d85c4-122">다음 표에 hello의 hello 링크를 클릭 하 여 자세한 정보:</span><span class="sxs-lookup"><span data-stu-id="d85c4-122">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="d85c4-123">작업</span><span class="sxs-lookup"><span data-stu-id="d85c4-123">Task</span></span> | <span data-ttu-id="d85c4-124">학습 내용</span><span class="sxs-lookup"><span data-stu-id="d85c4-124">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="d85c4-125">Azure DevTest Labs에서 랩 만들기</span><span class="sxs-lookup"><span data-stu-id="d85c4-125">Create a lab in Azure DevTest Labs</span></span>](devtest-lab-create-lab.md) |<span data-ttu-id="d85c4-126">Toocreate 랩에서 DevTest Labs를 Azure에는 Azure 포털 hello 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d85c4-126">Learn how toocreate a lab in Azure DevTest Labs in hello Azure portal.</span></span> |
2. <span data-ttu-id="d85c4-127">**바로 사용할 수 있는 마켓플레이스 이미지 및 사용자 지정 이미지를 사용하여 몇 분 만에 학습 VM 만들기**</span><span class="sxs-lookup"><span data-stu-id="d85c4-127">**Create training VMs in minutes using ready-made marketplace images and custom images**</span></span> 
   
    <span data-ttu-id="d85c4-128">Hello Azure Marketplace에서에서 다양 한 이미지에서에서 즉시 사용 가능한 이미지를 선택 하 고 hello 랩에서 hello 교육에 사용할 수 있도록 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d85c4-128">You can pick ready-made images from a wide variety of images in hello Azure Marketplace and make them available for hello trainees in hello lab.</span></span> <span data-ttu-id="d85c4-129">즉시 사용 가능한 이미지 hello 요구 사항을 충족 하지 않는 경우에 랩 hello 랩의 사용자 지정 이미지로 hello VM 저장 하 고 hello 학습에 필요한 모든 hello 소프트웨어를 설치 하는 Azure 마켓플레이스의 즉시 사용 가능한 이미지를 사용 하 여 VM을 만들어 사용자 지정 이미지를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d85c4-129">If hello ready-made images don't meet your requirements, you can create a custom image by creating a lab VM using a ready-made image from Azure Marketplace, installing all hello software that you need for hello training, and saving hello VM as custom image in hello lab.</span></span> 
   
    <span data-ttu-id="d85c4-130">다음 표에 hello의 hello 링크를 클릭 하 여 자세한 정보:</span><span class="sxs-lookup"><span data-stu-id="d85c4-130">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="d85c4-131">작업</span><span class="sxs-lookup"><span data-stu-id="d85c4-131">Task</span></span> | <span data-ttu-id="d85c4-132">학습 내용</span><span class="sxs-lookup"><span data-stu-id="d85c4-132">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="d85c4-133">Azure Marketplace 이미지 구성</span><span class="sxs-lookup"><span data-stu-id="d85c4-133">Configure Azure Marketplace images</span></span>](devtest-lab-configure-marketplace-images.md) |<span data-ttu-id="d85c4-134">화이트 리스트 Azure 마켓플레이스 이미지; 방법을 알아봅니다 hello 학습에 사용할 선택만 hello 이미지에 대 한 사용 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="d85c4-134">Learn how you can whitelist Azure Marketplace images; making available for selection only hello images you want for hello training.</span></span> |
   | [<span data-ttu-id="d85c4-135">사용자 지정 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="d85c4-135">Create a custom image</span></span>](devtest-lab-create-template.md) |<span data-ttu-id="d85c4-136">사전 교육 hello 사용자 지정 이미지를 사용 하는 VM을 신속 하 게 만들 수 있도록 hello 학습에 필요한 hello 소프트웨어를 설치 하 여 사용자 지정 이미지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d85c4-136">Create a custom image by pre-installing hello software you need for hello training so that trainees can quickly create a VM using hello custom image.</span></span> |
3. <span data-ttu-id="d85c4-137">**학습용 컴퓨터에 대한 재사용 가능 템플릿 만들기**</span><span class="sxs-lookup"><span data-stu-id="d85c4-137">**Create reusable templates for training machines**</span></span> 
   
    <span data-ttu-id="d85c4-138">Azure DevTest Labs의 수식에서는 toocreate VM을 사용 하는 기본 속성 값의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="d85c4-138">A formula in Azure DevTest Labs is a list of default property values used toocreate a VM.</span></span> <span data-ttu-id="d85c4-139">이미지, VM 크기 (CPU 및 RAM의 조합), 및 가상 네트워크를 선택 하 여 hello 랩에서 수식을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d85c4-139">You can create a formula in hello lab by picking an image, a VM size (a combination of CPU and RAM), and a virtual network.</span></span> <span data-ttu-id="d85c4-140">각 학습자 hello 랩에서 hello 수식을 보고 toocreate VM을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d85c4-140">Each trainee can see hello formula in hello lab and use it toocreate a VM.</span></span> 
   
    <span data-ttu-id="d85c4-141">다음 표에 hello의 hello 링크를 클릭 하 여 자세한 정보:</span><span class="sxs-lookup"><span data-stu-id="d85c4-141">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="d85c4-142">작업</span><span class="sxs-lookup"><span data-stu-id="d85c4-142">Task</span></span> | <span data-ttu-id="d85c4-143">학습 내용</span><span class="sxs-lookup"><span data-stu-id="d85c4-143">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="d85c4-144">DevTest Labs 수식 toocreate Vm 관리</span><span class="sxs-lookup"><span data-stu-id="d85c4-144">Manage DevTest Labs formulas toocreate VMs</span></span>](devtest-lab-manage-formulas.md) |<span data-ttu-id="d85c4-145">이미지, VM 크기(CPU와 RAM의 조합) 및 가상 네트워크를 선택하여 수식을 만들 수 있는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d85c4-145">Learn how you can create a formula by picking up an image, VM size (combination of CPU and RAM), and a virtual network.</span></span> |
4. <span data-ttu-id="d85c4-146">**비용 제어**</span><span class="sxs-lookup"><span data-stu-id="d85c4-146">**Control costs**</span></span>
   
    <span data-ttu-id="d85c4-147">DevTest Labs를 azure에 hello 랩 toospecify hello 최대 Vm 수 hello 랩에서 학습자에서 만들 수 있는 정책을 tooset를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d85c4-147">Azure DevTest Labs allows you tooset a policy in hello lab toospecify hello maximum number of VMs that can be created by a trainee in hello lab.</span></span> 
   
    <span data-ttu-id="d85c4-148">여러 날 학습을 수행 하는 고 toostop 모든 hello Vm hello 하루 중 특정 시간에 원하는 다음 자동으로 다시 시작 날짜를 다음 hello 쉽게 자동 종료를 설정 하 여이 수행 하 고 수 hello 랩에서 정책 자동으로 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="d85c4-148">If you are conducting multi-day training and want toostop all hello VMs at a particular time of hello day and then automatically restart them hello following day, you can easily accomplish that by setting auto-shutdown and auto-start policies in hello lab.</span></span> 
   
    <span data-ttu-id="d85c4-149">마지막으로, 학습 완료 되 면 삭제할 수 있습니다 모든 hello Vm 한 번에 단일 PowerShell 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d85c4-149">Finally, when training is complete you can delete all hello VMs at once by running a single PowerShell script.</span></span> 
   
    <span data-ttu-id="d85c4-150">다음 표에 hello의 hello 링크를 클릭 하 여 자세한 정보:</span><span class="sxs-lookup"><span data-stu-id="d85c4-150">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="d85c4-151">작업</span><span class="sxs-lookup"><span data-stu-id="d85c4-151">Task</span></span> | <span data-ttu-id="d85c4-152">학습 내용</span><span class="sxs-lookup"><span data-stu-id="d85c4-152">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="d85c4-153">랩 정책 정의</span><span class="sxs-lookup"><span data-stu-id="d85c4-153">Define lab policies</span></span>](devtest-lab-set-lab-policy.md) |<span data-ttu-id="d85c4-154">Hello 랩에서 정책을 설정 하 여 비용을 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="d85c4-154">Control costs by setting policies in hello lab.</span></span> |
   | [<span data-ttu-id="d85c4-155">모든 hello 랩 PowerShell 스크립트를 사용 하 여 Vm을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="d85c4-155">Delete all hello lab VMs using a PowerShell script</span></span>](devtest-lab-faq.md#how-can-i-automate-the-process-of-deleting-all-the-vms-in-my-lab) |<span data-ttu-id="d85c4-156">Hello 학습이 완료 될 때 한 번에 모든 hello labs를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="d85c4-156">Delete all hello labs in one operation when hello training is complete.</span></span> |
5. <span data-ttu-id="d85c4-157">**Hello 랩 각 학습자와 공유**</span><span class="sxs-lookup"><span data-stu-id="d85c4-157">**Share hello lab with each trainee**</span></span>
   
    <span data-ttu-id="d85c4-158">실습생과 공유하는 링크를 사용하여 랩에 직접 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d85c4-158">Labs can be directly accessed using a link that you share with your trainees.</span></span> <span data-ttu-id="d85c4-159">사용자 교육도 toohave는 Azure 계정이 없는 것으로 [Microsoft 계정](devtest-lab-faq.md#what-is-a-microsoft-account)합니다.</span><span class="sxs-lookup"><span data-stu-id="d85c4-159">Your trainees don't even have toohave an Azure account, as long as they have a [Microsoft account](devtest-lab-faq.md#what-is-a-microsoft-account).</span></span> <span data-ttu-id="d85c4-160">실습생은 다른 실습생이 만든 VM을 볼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d85c4-160">Trainees cannot see VMs created by other trainees.</span></span>  
   
    <span data-ttu-id="d85c4-161">다음 표에 hello의 hello 링크를 클릭 하 여 자세한 정보:</span><span class="sxs-lookup"><span data-stu-id="d85c4-161">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="d85c4-162">작업</span><span class="sxs-lookup"><span data-stu-id="d85c4-162">Task</span></span> | <span data-ttu-id="d85c4-163">학습 내용</span><span class="sxs-lookup"><span data-stu-id="d85c4-163">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="d85c4-164">학습자 tooa 랩 Azure DevTest Labs에 추가</span><span class="sxs-lookup"><span data-stu-id="d85c4-164">Add a trainee tooa lab in Azure DevTest Labs</span></span>](devtest-lab-add-devtest-user.md) |<span data-ttu-id="d85c4-165">Azure 포털 tooadd 교육 tooyour 교육 랩 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d85c4-165">Use hello Azure portal tooadd trainees tooyour training lab.</span></span> |
   | [<span data-ttu-id="d85c4-166">PowerShell 스크립트를 사용 하 여 교육 toohello 랩을 추가합니다</span><span class="sxs-lookup"><span data-stu-id="d85c4-166">Add trainees toohello lab using a PowerShell script</span></span>](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell) |<span data-ttu-id="d85c4-167">PowerShell tooautomate 교육 tooyour 교육 랩 추가 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d85c4-167">Use PowerShell tooautomate adding trainees tooyour training lab.</span></span> |
   | [<span data-ttu-id="d85c4-168">링크 toohello 랩 가져오기</span><span class="sxs-lookup"><span data-stu-id="d85c4-168">Get a link toohello lab</span></span>](devtest-lab-faq.md#how-do-i-share-a-direct-link-to-my-lab) |<span data-ttu-id="d85c4-169">하이퍼링크를 통해 랩에 바로 액세스할 수 있는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d85c4-169">Learn how a lab can be directly accessed via a hyperlink.</span></span> |
6. <span data-ttu-id="d85c4-170">**계속 해 서 hello 랩 다시 사용**</span><span class="sxs-lookup"><span data-stu-id="d85c4-170">**Reuse hello lab again and again**</span></span> 
   
    <span data-ttu-id="d85c4-171">사용자 지정 설정을 포함 하 여 리소스 관리자 템플릿을 만들어 사용 하 여 동일한 랩 toocreate 나중에 다시 랩 만들기를 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d85c4-171">You can automate lab creation, including custom settings, by creating a Resource Manager template and using it toocreate identical labs again and again.</span></span> 
   
    <span data-ttu-id="d85c4-172">다음 표에 hello의 hello 링크를 클릭 하 여 자세한 정보:</span><span class="sxs-lookup"><span data-stu-id="d85c4-172">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="d85c4-173">작업</span><span class="sxs-lookup"><span data-stu-id="d85c4-173">Task</span></span> | <span data-ttu-id="d85c4-174">학습 내용</span><span class="sxs-lookup"><span data-stu-id="d85c4-174">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="d85c4-175">Resource Manager 템플릿을 사용하여 랩 만들기</span><span class="sxs-lookup"><span data-stu-id="d85c4-175">Create a lab using a Resource Manager template</span></span>](devtest-lab-faq.md#how-do-i-create-a-lab-from-an-azure-resource-manager-template) |<span data-ttu-id="d85c4-176">Resource Manager 템플릿을 사용하여 Azure DevTest Labs에서 랩을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d85c4-176">Create labs in Azure DevTest Labs using Resource Manager templates.</span></span> |

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

