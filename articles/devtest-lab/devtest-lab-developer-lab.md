---
title: "개발자를 위한 Azure DevTest Labs 사용 | Microsoft Docs"
description: "개발자 시나리오에 Azure DevTest Labs를 사용하는 방법을 알아봅니다."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 22e070e5-3d1a-49fe-9d4c-5e07cb0b7fe2
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: tarcher
ms.openlocfilehash: c187819e9392908c8979556f80e8c94739eb14d5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-devtest-labs-for-developers"></a><span data-ttu-id="4262f-103">개발자를 위한 Azure DevTest Labs 사용</span><span class="sxs-lookup"><span data-stu-id="4262f-103">Use Azure DevTest Labs for developers</span></span>
<span data-ttu-id="4262f-104">Azure DevTest Labs를 사용하여 여러 주요 시나리오를 구현할 수 있지만 기본 시나리오 중 하나는 DevTest Labs를 사용하여 개발자를 위한 개발 컴퓨터를 호스트하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4262f-104">Azure DevTest Labs can be used to implement many key scenarios, but one of the primary scenarios involves using DevTest Labs to host development machines for developers.</span></span> <span data-ttu-id="4262f-105">이 시나리오에서는 DevTest Labs는 다음과 같은 이점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4262f-105">In this scenario, DevTest Labs provides these benefits:</span></span>

- <span data-ttu-id="4262f-106">개발자는 필요에 따라 개발 컴퓨터를 신속하게 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4262f-106">Developers can quickly provision their development machines on demand.</span></span>
- <span data-ttu-id="4262f-107">개발자는 필요할 때마다 개발 컴퓨터를 쉽게 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4262f-107">Developers can easily customize their development machines whenever needed.</span></span>
- <span data-ttu-id="4262f-108">관리자는 다음을 확인하여 비용을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4262f-108">Administrators can control costs by ensuring that:</span></span>
  - <span data-ttu-id="4262f-109">개발자는 개발에 필요한 것보다 더 많은 VM을 가져올 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4262f-109">Developers cannot get more VMs than they need for development.</span></span>
  - <span data-ttu-id="4262f-110">VM은 사용되지 않을 때 종료됩니다.</span><span class="sxs-lookup"><span data-stu-id="4262f-110">VMs are shut down when not in use.</span></span> 

![학습에 DevTest Labs 사용](./media/devtest-lab-developer-lab/devtest-lab-developer-lab.png)

<span data-ttu-id="4262f-112">이 문서에서는 개발자 요구 사항을 충족하는 데 사용할 수 있는 여러 Azure DevTest Labs 기능과 랩을 설정하는 데 수행할 수 있는 자세한 단계에 대해 학습합니다.</span><span class="sxs-lookup"><span data-stu-id="4262f-112">In this article, you learn about various Azure DevTest Labs features that can be used to meet developer requirements and the detailed steps that you can follow to set up a lab.</span></span>

## <a name="implementing-developer-environments-with-azure-devtest-labs"></a><span data-ttu-id="4262f-113">Azure DevTest Labs를 사용하여 개발자 환경 구현</span><span class="sxs-lookup"><span data-stu-id="4262f-113">Implementing developer environments with Azure DevTest Labs</span></span>
1. <span data-ttu-id="4262f-114">**랩 만들기**</span><span class="sxs-lookup"><span data-stu-id="4262f-114">**Create the lab**</span></span> 
   
    <span data-ttu-id="4262f-115">랩은 Azure DevTest Labs의 시작 지점입니다.</span><span class="sxs-lookup"><span data-stu-id="4262f-115">Labs are the starting point in Azure DevTest Labs.</span></span> <span data-ttu-id="4262f-116">랩을 만든 후 랩에 사용자(개발자)를 추가하고, 비용을 제어하는 정책을 설정하고, 신속하게 만들 수 있는 VM 이미지를 정의하는 등의 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4262f-116">Once you create a lab, you can perform tasks such as adding users (developers) to the lab, setting policies to control costs, defining VM images that can create quickly, and more.</span></span>  
   
    <span data-ttu-id="4262f-117">다음 표에 있는 링크를 클릭하면 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4262f-117">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="4262f-118">작업</span><span class="sxs-lookup"><span data-stu-id="4262f-118">Task</span></span> | <span data-ttu-id="4262f-119">학습 내용</span><span class="sxs-lookup"><span data-stu-id="4262f-119">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="4262f-120">Azure DevTest Labs에서 랩 만들기</span><span class="sxs-lookup"><span data-stu-id="4262f-120">Create a lab in Azure DevTest Labs</span></span>](devtest-lab-create-lab.md) |<span data-ttu-id="4262f-121">Azure Portal의 Azure DevTest Labs에서 랩을 만드는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4262f-121">Learn how to create a lab in Azure DevTest Labs in the Azure portal.</span></span> |
2. <span data-ttu-id="4262f-122">**바로 사용할 수 있는 마켓플레이스 이미지 및 사용자 지정 이미지를 사용하여 몇 분 만에 VM 만들기**</span><span class="sxs-lookup"><span data-stu-id="4262f-122">**Create VMs in minutes using ready-made marketplace images and custom images**</span></span> 
   
    <span data-ttu-id="4262f-123">Azure Marketplace의 다양한 이미지에서 바로 사용할 수 있는 이미지를 선택하고 랩에서 사용하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4262f-123">You can pick ready-made images from a wide variety of images in the Azure Marketplace and make them available in the lab.</span></span> <span data-ttu-id="4262f-124">바로 사용할 수 있는 이미지가 요구 사항을 충족하지 않을 경우 Azure Marketplace에서 바로 사용할 수 있는 이미지를 사용하여 랩 VM을 만들고, 필요한 모든 소프트웨어를 설치하고, 랩의 사용자 지정 이미지로 VM을 지정함으로써 사용자 지정 이미지를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4262f-124">If the ready-made images don't meet your requirements, you can create a custom image by creating a lab VM using a ready-made image from Azure Marketplace, installing all the software that you need, and saving the VM as a custom image in the lab.</span></span>

    <span data-ttu-id="4262f-125">사용자 지정 이미지를 사용하는 경우 이미지 팩터리를 사용하여 이미지를 만들고 배포하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4262f-125">If you will be using custom images, consider using an image factory to create and distribute your images.</span></span> <span data-ttu-id="4262f-126">이미지 팩터리는 구성된 이미지를 자동으로 정기적으로 작성 및 배포하는 "코드로 구성" 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="4262f-126">An image factory is a configuration-as-code solution that regularly builds and distributes your configured images automatically.</span></span> <span data-ttu-id="4262f-127">이를 사용하면 VM을 기본 OS로 만든 후에 시스템을 수동으로 구성하는 데 필요한 시간이 절감됩니다.</span><span class="sxs-lookup"><span data-stu-id="4262f-127">This saves the time required to manually configure the system after a VM has been created with the base OS.</span></span>
  
    <span data-ttu-id="4262f-128">다음 표에 있는 링크를 클릭하면 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4262f-128">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="4262f-129">작업</span><span class="sxs-lookup"><span data-stu-id="4262f-129">Task</span></span> | <span data-ttu-id="4262f-130">학습 내용</span><span class="sxs-lookup"><span data-stu-id="4262f-130">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="4262f-131">Azure Marketplace 이미지 구성</span><span class="sxs-lookup"><span data-stu-id="4262f-131">Configure Azure Marketplace images</span></span>](devtest-lab-configure-marketplace-images.md) |<span data-ttu-id="4262f-132">개발자용으로 원하는 이미지만 선택할 수 있도록 Azure Marketplace 이미지를 허용 목록에 추가할 수 있는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4262f-132">Learn how you can whitelist Azure Marketplace images, making available for selection only the images you want for the developers.</span></span>|
   | [<span data-ttu-id="4262f-133">사용자 지정 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="4262f-133">Create a custom image</span></span>](devtest-lab-create-template.md) |<span data-ttu-id="4262f-134">개발자가 사용자 지정 이미지를 사용하여 신속하게 VM을 만들 수 있도록 필요한 소프트웨어를 미리 설치하여 사용자 지정 이미지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4262f-134">Create a custom image by pre-installing the software you need so that developers can quickly create a VM using the custom image.</span></span>|
   | [<span data-ttu-id="4262f-135">이미지 팩터리에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="4262f-135">Learn about image factory</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2017/04/17/video-custom-image-factory-with-azure-devtest-labs/) |<span data-ttu-id="4262f-136">이미지 팩터리를 설정 및 사용하는 방법을 설명하는 비디오를 시청하세요.</span><span class="sxs-lookup"><span data-stu-id="4262f-136">Watch a video that describes how to set up and use an image factory.</span></span>|

3. <span data-ttu-id="4262f-137">**개발자 컴퓨터에 대한 재사용 가능 템플릿 만들기**</span><span class="sxs-lookup"><span data-stu-id="4262f-137">**Create reusable templates for developer machines**</span></span> 
   
    <span data-ttu-id="4262f-138">Azure DevTest Labs의 수식은 VM을 만드는 데 사용되는 기본 속성 값의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="4262f-138">A formula in Azure DevTest Labs is a list of default property values used to create a VM.</span></span> <span data-ttu-id="4262f-139">이미지, VM 크기(CPU와 RAM의 조합) 및 가상 네트워크를 선택하여 랩에서 수식을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4262f-139">You can create a formula in the lab by picking an image, a VM size (a combination of CPU and RAM), and a virtual network.</span></span> <span data-ttu-id="4262f-140">각 개발자는 랩에서 수식을 보고 수식을 사용하여 VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4262f-140">Each developer can see the formula in the lab and use it to create a VM.</span></span> 
   
    <span data-ttu-id="4262f-141">다음 표에 있는 링크를 클릭하면 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4262f-141">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="4262f-142">작업</span><span class="sxs-lookup"><span data-stu-id="4262f-142">Task</span></span> | <span data-ttu-id="4262f-143">학습 내용</span><span class="sxs-lookup"><span data-stu-id="4262f-143">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="4262f-144">VM을 만드는 DevTest Labs 수식 관리</span><span class="sxs-lookup"><span data-stu-id="4262f-144">Manage DevTest Labs formulas to create VMs</span></span>](devtest-lab-manage-formulas.md) |<span data-ttu-id="4262f-145">이미지, VM 크기(CPU와 RAM의 조합) 및 가상 네트워크를 선택하여 수식을 만들 수 있는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4262f-145">Learn how you can create a formula by picking up an image, VM size (combination of CPU and RAM), and a virtual network.</span></span>|

4. <span data-ttu-id="4262f-146">**아티팩트를 만들어 유연한 VM 사용자 지정 사용**</span><span class="sxs-lookup"><span data-stu-id="4262f-146">**Create artifacts to enable flexible VM customization**</span></span>

   <span data-ttu-id="4262f-147">VM이 프로비전된 후 응용 프로그램을 배포하고 구성하기 위해 아티팩트가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4262f-147">Artifacts are used to deploy and configure your application after a VM is provisioned.</span></span> <span data-ttu-id="4262f-148">아티팩트는 다음과 같을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4262f-148">Artifacts can be:</span></span>

   - <span data-ttu-id="4262f-149">VM에 설치하려는 도구(예: 에이전트, Fiddler 및 Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="4262f-149">Tools that you want to install on the VM - such as agents, Fiddler, and Visual Studio.</span></span>
   - <span data-ttu-id="4262f-150">VM에서 실행하려는 작업(예: 리포지토리 복제)</span><span class="sxs-lookup"><span data-stu-id="4262f-150">Actions that you want to run on the VM - such as cloning a repo.</span></span>
   - <span data-ttu-id="4262f-151">테스트하려는 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="4262f-151">Applications that you want to test.</span></span>

   <span data-ttu-id="4262f-152">많은 아티팩트는 이미 기본 제공되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4262f-152">Many artifacts are already available out-of-the-box.</span></span> <span data-ttu-id="4262f-153">특정 요구에 맞게 추가로 사용자 지정하려는 경우 사용자 고유의 사용자 지정 아티팩트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4262f-153">You can create your own custom artifacts if you want more customization for your specific needs.</span></span>

   <span data-ttu-id="4262f-154">다음 표에 있는 링크를 클릭하면 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4262f-154">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="4262f-155">작업</span><span class="sxs-lookup"><span data-stu-id="4262f-155">Task</span></span> | <span data-ttu-id="4262f-156">학습 내용</span><span class="sxs-lookup"><span data-stu-id="4262f-156">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="4262f-157">DevTest Lab VM에 대한 사용자 지정 아티팩트 만들기</span><span class="sxs-lookup"><span data-stu-id="4262f-157">Create custom artifacts for your DevTest Labs VM</span></span>](devtest-lab-artifact-author.md) |<span data-ttu-id="4262f-158">랩에서 가상 컴퓨터에 대한 사용자 고유의 사용자 지정 아티팩트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4262f-158">Create your own custom artifacts for the virtual machines in your lab.</span></span>|
   | [<span data-ttu-id="4262f-159">Azure DevTest Labs에서 사용하기 위한 사용자 지정 아티팩트 및 Azure Resource Manager 템플릿을 저장할 Git 리포지토리 추가</span><span class="sxs-lookup"><span data-stu-id="4262f-159">Add a Git repository to store custom artifacts and Azure Resource Manager templates for use in Azure DevTest Labs</span></span>](devtest-lab-add-artifact-repo.md) |<span data-ttu-id="4262f-160">사용자 지정 아티팩트를 자체의 개인 Git 리포지토리에 저장하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4262f-160">Learn how to store your custom artifacts in your own private Git repo.</span></span>|

5. <span data-ttu-id="4262f-161">**비용 제어**</span><span class="sxs-lookup"><span data-stu-id="4262f-161">**Control costs**</span></span>
   
    <span data-ttu-id="4262f-162">Azure DevTest Labs를 통해 랩에서 개발자가 만들 수 있는 VM의 최대 수를 지정하는 정책을 랩에 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4262f-162">Azure DevTest Labs allows you to set a policy in the lab to specify the maximum number of VMs that can be created by a developer in the lab.</span></span> 
   
    <span data-ttu-id="4262f-163">개발자 팀에 설정된 작업 일정이 있고 하루 중 특정 시간에 모든 VM을 중지했다가 다음 날 자동으로 다시 시작하도록 하려면 랩에서 자동 종료 및 자동 시작 정책을 설정하여 쉽게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4262f-163">If your developer team has a set work schedule and you want to stop all the VMs at a particular time of the day and then automatically restart them the following day, you can easily accomplish that by setting auto-shutdown and auto-start policies in the lab.</span></span> 
   
    <span data-ttu-id="4262f-164">마지막으로 앱 개발이 완료되면 단일 PowerShell 스크립트를 실행하여 모든 VM을 한 번에 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4262f-164">Finally, when app development is complete, you can delete all the VMs at once by running a single PowerShell script.</span></span> 
   
    <span data-ttu-id="4262f-165">다음 표에 있는 링크를 클릭하면 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4262f-165">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="4262f-166">작업</span><span class="sxs-lookup"><span data-stu-id="4262f-166">Task</span></span> | <span data-ttu-id="4262f-167">학습 내용</span><span class="sxs-lookup"><span data-stu-id="4262f-167">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="4262f-168">랩 정책 정의</span><span class="sxs-lookup"><span data-stu-id="4262f-168">Define lab policies</span></span>](devtest-lab-set-lab-policy.md) |<span data-ttu-id="4262f-169">랩에 정책을 설정하여 비용을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="4262f-169">Control costs by setting policies in the lab.</span></span> |
   | [<span data-ttu-id="4262f-170">PowerShell 스크립트를 사용하여 모든 랩 VM 삭제</span><span class="sxs-lookup"><span data-stu-id="4262f-170">Delete all the lab VMs using a PowerShell script</span></span>](devtest-lab-faq.md#how-can-i-automate-the-process-of-deleting-all-the-vms-in-my-lab) |<span data-ttu-id="4262f-171">개발이 완료되면 한 번에 모든 랩을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="4262f-171">Delete all the labs in one operation when development is complete.</span></span>|

1. <span data-ttu-id="4262f-172">**VM에 가상 네트워크 추가**</span><span class="sxs-lookup"><span data-stu-id="4262f-172">**Add a virtual network to a VM**</span></span> 
   
    <span data-ttu-id="4262f-173">DevTest Labs는 랩이 생성될 때마다 새 VNET(가상 네트워크)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4262f-173">DevTest Labs creates a new virtual network (VNET) whenever a lab is created.</span></span> <span data-ttu-id="4262f-174">예를 들어 ExpressRoute 또는 사이트 간 VPN을 사용하여 사용자 고유의 VNET을 구성한 경우 VM을 만들 때 사용할 수 있도록 랩의 가상 네트워크 설정에 이 VNET을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4262f-174">If you have configured your own VNET – for example, by using ExpressRoute or site-to-site VPN – you can add this VNET to your lab's virtual network settings so that it is available when creating VMs.</span></span>

    <span data-ttu-id="4262f-175">또한 VM이 만들어질 때 VM을 도메인에 가입하는 Azure Active Directory 도메인 가입 아티팩트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4262f-175">In addition, there is an Azure Active Directory domain join artifact available that will join a VM to a domain when the VM is being created.</span></span> 
   
    <span data-ttu-id="4262f-176">다음 표에 있는 링크를 클릭하면 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4262f-176">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="4262f-177">작업</span><span class="sxs-lookup"><span data-stu-id="4262f-177">Task</span></span> | <span data-ttu-id="4262f-178">학습 내용</span><span class="sxs-lookup"><span data-stu-id="4262f-178">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="4262f-179">Azure DevTest Labs에서 가상 네트워크 구성</span><span class="sxs-lookup"><span data-stu-id="4262f-179">Configure a virtual network in Azure DevTest Labs</span></span>](devtest-lab-configure-vnet.md) |<span data-ttu-id="4262f-180">Azure Portal을 사용하여 Azure DevTest Labs에서 가상 네트워크를 구성하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4262f-180">Learn how to configure a virtual network in Azure DevTest Labs using the Azure portal.</span></span>|

6. <span data-ttu-id="4262f-181">**각 개발자와 랩 공유**</span><span class="sxs-lookup"><span data-stu-id="4262f-181">**Share the lab with each developer**</span></span>
   
    <span data-ttu-id="4262f-182">개발자와 공유하는 링크를 사용하여 랩에 직접 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4262f-182">Labs can be directly accessed using a link that you share with your developers.</span></span> <span data-ttu-id="4262f-183">[Microsoft 계정](devtest-lab-faq.md#what-is-a-microsoft-account)이 있는 개발자는 Azure 계정이 없어도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4262f-183">They don't even have to have an Azure account, as long as they have a [Microsoft account](devtest-lab-faq.md#what-is-a-microsoft-account).</span></span> <span data-ttu-id="4262f-184">개발자는 다른 개발자가 만든 VM을 볼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4262f-184">Developers cannot see VMs created by other developers.</span></span>  
   
    <span data-ttu-id="4262f-185">다음 표에 있는 링크를 클릭하면 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4262f-185">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="4262f-186">작업</span><span class="sxs-lookup"><span data-stu-id="4262f-186">Task</span></span> | <span data-ttu-id="4262f-187">학습 내용</span><span class="sxs-lookup"><span data-stu-id="4262f-187">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="4262f-188">Azure DevTest Labs에서 랩에 개발자 추가</span><span class="sxs-lookup"><span data-stu-id="4262f-188">Add a developer to a lab in Azure DevTest Labs</span></span>](devtest-lab-add-devtest-user.md) |<span data-ttu-id="4262f-189">랩에 개발자를 추가하려면 Azure Portal을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4262f-189">Use the Azure portal to add developers to your lab.</span></span>|
   | [<span data-ttu-id="4262f-190">PowerShell 스크립트를 사용하여 랩에 개발자 추가</span><span class="sxs-lookup"><span data-stu-id="4262f-190">Add developers to the lab using a PowerShell script</span></span>](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell) |<span data-ttu-id="4262f-191">PowerShell을 사용하여 랩에 개발자를 자동으로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4262f-191">Use PowerShell to automate adding developers to your lab.</span></span> |
   | [<span data-ttu-id="4262f-192">랩에 대한 링크 가져오기</span><span class="sxs-lookup"><span data-stu-id="4262f-192">Get a link to the lab</span></span>](devtest-lab-faq.md#how-do-i-share-a-direct-link-to-my-lab) |<span data-ttu-id="4262f-193">개발자가 하이퍼링크를 통해 랩에 직접 액세스하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4262f-193">Learn how developers can directly access a lab via a hyperlink.</span></span>|

7. <span data-ttu-id="4262f-194">**추가 팀을 위한 랩 생성 자동화**</span><span class="sxs-lookup"><span data-stu-id="4262f-194">**Automate lab creation for more teams**</span></span> 
   
    <span data-ttu-id="4262f-195">Resource Manager 템플릿을 만들어 동일한 랩을 반복해서 다시 만드는 데 사용하면 사용자 지정 설정을 포함하여 랩 만들기를 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4262f-195">You can automate lab creation, including custom settings, by creating a Resource Manager template and using it to create identical labs again and again.</span></span> 
   
    <span data-ttu-id="4262f-196">다음 표에 있는 링크를 클릭하면 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4262f-196">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="4262f-197">작업</span><span class="sxs-lookup"><span data-stu-id="4262f-197">Task</span></span> | <span data-ttu-id="4262f-198">학습 내용</span><span class="sxs-lookup"><span data-stu-id="4262f-198">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="4262f-199">Resource Manager 템플릿을 사용하여 랩 만들기</span><span class="sxs-lookup"><span data-stu-id="4262f-199">Create a lab using a Resource Manager template</span></span>](devtest-lab-faq.md#how-do-i-create-a-lab-from-an-azure-resource-manager-template) |<span data-ttu-id="4262f-200">Resource Manager 템플릿을 사용하여 Azure DevTest Labs에서 랩을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4262f-200">Create labs in Azure DevTest Labs using Resource Manager templates.</span></span> |

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

