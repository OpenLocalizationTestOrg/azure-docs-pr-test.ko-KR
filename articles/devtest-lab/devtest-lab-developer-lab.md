---
title: "개발자를 위한 Azure DevTest Labs aaaUse | Microsoft Docs"
description: "자세한 내용은 방법 toouse Azure DevTest Labs 개발자 시나리오용입니다."
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
ms.openlocfilehash: 16a3ef47c9fcbca3050dd50db5b472a9a1e3c62c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-devtest-labs-for-developers"></a><span data-ttu-id="9f1f5-103">개발자를 위한 Azure DevTest Labs 사용</span><span class="sxs-lookup"><span data-stu-id="9f1f5-103">Use Azure DevTest Labs for developers</span></span>
<span data-ttu-id="9f1f5-104">DevTest Labs azure 개발자를 위한 DevTest Labs toohost 개발 컴퓨터를 사용 하 여 여러 주요 시나리오 중 하나 hello 기본 시나리오 중 하나를 사용 하는 tooimplement 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f1f5-104">Azure DevTest Labs can be used tooimplement many key scenarios, but one of hello primary scenarios involves using DevTest Labs toohost development machines for developers.</span></span> <span data-ttu-id="9f1f5-105">이 시나리오에서 DevTest Labs는 다음과 같은 이점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9f1f5-105">In this scenario, DevTest Labs provides these benefits:</span></span>

- <span data-ttu-id="9f1f5-106">개발자는 필요에 따라 개발 컴퓨터를 신속하게 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f1f5-106">Developers can quickly provision their development machines on demand.</span></span>
- <span data-ttu-id="9f1f5-107">개발자는 필요할 때마다 개발 컴퓨터를 쉽게 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f1f5-107">Developers can easily customize their development machines whenever needed.</span></span>
- <span data-ttu-id="9f1f5-108">관리자는 다음을 확인하여 비용을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f1f5-108">Administrators can control costs by ensuring that:</span></span>
  - <span data-ttu-id="9f1f5-109">개발자는 개발에 필요한 것보다 더 많은 VM을 가져올 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9f1f5-109">Developers cannot get more VMs than they need for development.</span></span>
  - <span data-ttu-id="9f1f5-110">VM은 사용되지 않을 때 종료됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f1f5-110">VMs are shut down when not in use.</span></span> 

![학습에 DevTest Labs 사용](./media/devtest-lab-developer-lab/devtest-lab-developer-lab.png)

<span data-ttu-id="9f1f5-112">이 문서에서는 사용 되는 toomeet 개발자 요구 사항 및 랩을 tooset를 따를 수 하는 자세한 단계 hello 수 있는 다양 한 Azure DevTest Labs 기능에 대 한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="9f1f5-112">In this article, you learn about various Azure DevTest Labs features that can be used toomeet developer requirements and hello detailed steps that you can follow tooset up a lab.</span></span>

## <a name="implementing-developer-environments-with-azure-devtest-labs"></a><span data-ttu-id="9f1f5-113">Azure DevTest Labs를 사용하여 개발자 환경 구현</span><span class="sxs-lookup"><span data-stu-id="9f1f5-113">Implementing developer environments with Azure DevTest Labs</span></span>
1. <span data-ttu-id="9f1f5-114">**Hello 랩 만들기**</span><span class="sxs-lookup"><span data-stu-id="9f1f5-114">**Create hello lab**</span></span> 
   
    <span data-ttu-id="9f1f5-115">랩은 hello Azure DevTest Labs의 시작 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="9f1f5-115">Labs are hello starting point in Azure DevTest Labs.</span></span> <span data-ttu-id="9f1f5-116">랩을 만든 후 사용자 (개발자) toohello 랩, 설정 정책 toocontrol 비용을 신속 하 게 만들 수 있는 VM 이미지를 정의 및 추가 같은 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f1f5-116">Once you create a lab, you can perform tasks such as adding users (developers) toohello lab, setting policies toocontrol costs, defining VM images that can create quickly, and more.</span></span>  
   
    <span data-ttu-id="9f1f5-117">다음 표에 hello의 hello 링크를 클릭 하 여 자세한 정보:</span><span class="sxs-lookup"><span data-stu-id="9f1f5-117">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="9f1f5-118">작업</span><span class="sxs-lookup"><span data-stu-id="9f1f5-118">Task</span></span> | <span data-ttu-id="9f1f5-119">학습 내용</span><span class="sxs-lookup"><span data-stu-id="9f1f5-119">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="9f1f5-120">Azure DevTest Labs에서 랩 만들기</span><span class="sxs-lookup"><span data-stu-id="9f1f5-120">Create a lab in Azure DevTest Labs</span></span>](devtest-lab-create-lab.md) |<span data-ttu-id="9f1f5-121">Toocreate 랩에서 DevTest Labs를 Azure에는 Azure 포털 hello 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="9f1f5-121">Learn how toocreate a lab in Azure DevTest Labs in hello Azure portal.</span></span> |
2. <span data-ttu-id="9f1f5-122">**바로 사용할 수 있는 마켓플레이스 이미지 및 사용자 지정 이미지를 사용하여 몇 분 만에 VM 만들기**</span><span class="sxs-lookup"><span data-stu-id="9f1f5-122">**Create VMs in minutes using ready-made marketplace images and custom images**</span></span> 
   
    <span data-ttu-id="9f1f5-123">Hello Azure Marketplace에서에서 다양 한 이미지에서에서 즉시 사용 가능한 이미지를 선택 하 고 hello 랩에서 사용할 수 있도록 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f1f5-123">You can pick ready-made images from a wide variety of images in hello Azure Marketplace and make them available in hello lab.</span></span> <span data-ttu-id="9f1f5-124">Hello 즉시 사용 가능한 이미지 요구 사항을 충족 하지 않는 경우에 랩 hello 랩에 대 한 사용자 지정 이미지로 Azure 마켓플레이스를 필요한 모든 hello 소프트웨어를 설치 하 고 저장 하는 hello VM에서 이미 만들어진 이미지를 사용 하 여 VM을 만들어 사용자 지정 이미지를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f1f5-124">If hello ready-made images don't meet your requirements, you can create a custom image by creating a lab VM using a ready-made image from Azure Marketplace, installing all hello software that you need, and saving hello VM as a custom image in hello lab.</span></span>

    <span data-ttu-id="9f1f5-125">사용자 지정 이미지를 사용 하는 경우 이미지 팩터리 toocreate를 사용 하 여 분산 하 여 이미지 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f1f5-125">If you will be using custom images, consider using an image factory toocreate and distribute your images.</span></span> <span data-ttu-id="9f1f5-126">이미지 팩터리는 구성된 이미지를 자동으로 정기적으로 작성 및 배포하는 "코드로 구성" 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="9f1f5-126">An image factory is a configuration-as-code solution that regularly builds and distributes your configured images automatically.</span></span> <span data-ttu-id="9f1f5-127">이 저장 hello 필요한 시간 toomanually hello로 VM이 만들어진 후 hello 시스템 구성 운영 체제를 기반 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f1f5-127">This saves hello time required toomanually configure hello system after a VM has been created with hello base OS.</span></span>
  
    <span data-ttu-id="9f1f5-128">다음 표에 hello의 hello 링크를 클릭 하 여 자세한 정보:</span><span class="sxs-lookup"><span data-stu-id="9f1f5-128">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="9f1f5-129">작업</span><span class="sxs-lookup"><span data-stu-id="9f1f5-129">Task</span></span> | <span data-ttu-id="9f1f5-130">학습 내용</span><span class="sxs-lookup"><span data-stu-id="9f1f5-130">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="9f1f5-131">Azure Marketplace 이미지 구성</span><span class="sxs-lookup"><span data-stu-id="9f1f5-131">Configure Azure Marketplace images</span></span>](devtest-lab-configure-marketplace-images.md) |<span data-ttu-id="9f1f5-132">방법을 알아봅니다 화이트 리스트 Azure 마켓플레이스 이미지 hello 개발자를 위한 원하는 선택만 hello 이미지를 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f1f5-132">Learn how you can whitelist Azure Marketplace images, making available for selection only hello images you want for hello developers.</span></span>|
   | [<span data-ttu-id="9f1f5-133">사용자 지정 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="9f1f5-133">Create a custom image</span></span>](devtest-lab-create-template.md) |<span data-ttu-id="9f1f5-134">사전 개발자 hello 사용자 지정 이미지를 사용 하는 VM을 신속 하 게 만들 수 있도록 해야 하는 hello 소프트웨어를 설치 하 여 사용자 지정 이미지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9f1f5-134">Create a custom image by pre-installing hello software you need so that developers can quickly create a VM using hello custom image.</span></span>|
   | [<span data-ttu-id="9f1f5-135">이미지 팩터리에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="9f1f5-135">Learn about image factory</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2017/04/17/video-custom-image-factory-with-azure-devtest-labs/) |<span data-ttu-id="9f1f5-136">설명 하는 비디오를 시청 방법을 tooset 및 이미지 팩터리를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f1f5-136">Watch a video that describes how tooset up and use an image factory.</span></span>|

3. <span data-ttu-id="9f1f5-137">**개발자 컴퓨터에 대한 재사용 가능 템플릿 만들기**</span><span class="sxs-lookup"><span data-stu-id="9f1f5-137">**Create reusable templates for developer machines**</span></span> 
   
    <span data-ttu-id="9f1f5-138">Azure DevTest Labs의 수식에서는 toocreate VM을 사용 하는 기본 속성 값의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="9f1f5-138">A formula in Azure DevTest Labs is a list of default property values used toocreate a VM.</span></span> <span data-ttu-id="9f1f5-139">이미지, VM 크기 (CPU 및 RAM의 조합), 및 가상 네트워크를 선택 하 여 hello 랩에서 수식을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f1f5-139">You can create a formula in hello lab by picking an image, a VM size (a combination of CPU and RAM), and a virtual network.</span></span> <span data-ttu-id="9f1f5-140">각 개발자 hello 랩에서 hello 수식을 보고 toocreate VM을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f1f5-140">Each developer can see hello formula in hello lab and use it toocreate a VM.</span></span> 
   
    <span data-ttu-id="9f1f5-141">다음 표에 hello의 hello 링크를 클릭 하 여 자세한 정보:</span><span class="sxs-lookup"><span data-stu-id="9f1f5-141">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="9f1f5-142">작업</span><span class="sxs-lookup"><span data-stu-id="9f1f5-142">Task</span></span> | <span data-ttu-id="9f1f5-143">학습 내용</span><span class="sxs-lookup"><span data-stu-id="9f1f5-143">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="9f1f5-144">DevTest Labs 수식 toocreate Vm 관리</span><span class="sxs-lookup"><span data-stu-id="9f1f5-144">Manage DevTest Labs formulas toocreate VMs</span></span>](devtest-lab-manage-formulas.md) |<span data-ttu-id="9f1f5-145">이미지, VM 크기(CPU와 RAM의 조합) 및 가상 네트워크를 선택하여 수식을 만들 수 있는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="9f1f5-145">Learn how you can create a formula by picking up an image, VM size (combination of CPU and RAM), and a virtual network.</span></span>|

4. <span data-ttu-id="9f1f5-146">**아티팩트 tooenable 유연한 VM 사용자 지정 만들기**</span><span class="sxs-lookup"><span data-stu-id="9f1f5-146">**Create artifacts tooenable flexible VM customization**</span></span>

   <span data-ttu-id="9f1f5-147">아티팩트는 사용 되는 toodeploy 및 VM 프로 비전 된 후 응용 프로그램을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f1f5-147">Artifacts are used toodeploy and configure your application after a VM is provisioned.</span></span> <span data-ttu-id="9f1f5-148">아티팩트는 다음과 같을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f1f5-148">Artifacts can be:</span></span>

   - <span data-ttu-id="9f1f5-149">에이전트, Fiddler 및 Visual Studio와 같은 VM-hello에 tooinstall 원하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="9f1f5-149">Tools that you want tooinstall on hello VM - such as agents, Fiddler, and Visual Studio.</span></span>
   - <span data-ttu-id="9f1f5-150">리포지토리 복제 같은 VM-hello에 toorun 되도록 동작입니다.</span><span class="sxs-lookup"><span data-stu-id="9f1f5-150">Actions that you want toorun on hello VM - such as cloning a repo.</span></span>
   - <span data-ttu-id="9f1f5-151">응용 프로그램 tootest 한다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9f1f5-151">Applications that you want tootest.</span></span>

   <span data-ttu-id="9f1f5-152">많은 아티팩트는 이미 기본 제공되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f1f5-152">Many artifacts are already available out-of-the-box.</span></span> <span data-ttu-id="9f1f5-153">특정 요구에 맞게 추가로 사용자 지정하려는 경우 사용자 고유의 사용자 지정 아티팩트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f1f5-153">You can create your own custom artifacts if you want more customization for your specific needs.</span></span>

   <span data-ttu-id="9f1f5-154">다음 표에 hello의 hello 링크를 클릭 하 여 자세한 정보:</span><span class="sxs-lookup"><span data-stu-id="9f1f5-154">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="9f1f5-155">작업</span><span class="sxs-lookup"><span data-stu-id="9f1f5-155">Task</span></span> | <span data-ttu-id="9f1f5-156">학습 내용</span><span class="sxs-lookup"><span data-stu-id="9f1f5-156">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="9f1f5-157">DevTest Lab VM에 대한 사용자 지정 아티팩트 만들기</span><span class="sxs-lookup"><span data-stu-id="9f1f5-157">Create custom artifacts for your DevTest Labs VM</span></span>](devtest-lab-artifact-author.md) |<span data-ttu-id="9f1f5-158">랩에서 hello 가상 컴퓨터에 대 한 사용자 고유의 사용자 지정 아티팩트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9f1f5-158">Create your own custom artifacts for hello virtual machines in your lab.</span></span>|
   | [<span data-ttu-id="9f1f5-159">Azure DevTest Labs에서 Git 리포지토리 toostore 사용자 지정 아티팩트 및 Azure 리소스 관리자 템플릿을 사용 하기 위해 추가</span><span class="sxs-lookup"><span data-stu-id="9f1f5-159">Add a Git repository toostore custom artifacts and Azure Resource Manager templates for use in Azure DevTest Labs</span></span>](devtest-lab-add-artifact-repo.md) |<span data-ttu-id="9f1f5-160">자세한 내용은 방법 toostore 자신의 개인 Git 리포지토리에 있는 사용자 지정 아티팩트입니다.</span><span class="sxs-lookup"><span data-stu-id="9f1f5-160">Learn how toostore your custom artifacts in your own private Git repo.</span></span>|

5. <span data-ttu-id="9f1f5-161">**비용 제어**</span><span class="sxs-lookup"><span data-stu-id="9f1f5-161">**Control costs**</span></span>
   
    <span data-ttu-id="9f1f5-162">DevTest Labs를 azure에 hello 랩 toospecify hello 최대 Vm 수 hello 랩에서 개발자가 만들 수 있는 정책을 tooset를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f1f5-162">Azure DevTest Labs allows you tooset a policy in hello lab toospecify hello maximum number of VMs that can be created by a developer in hello lab.</span></span> 
   
    <span data-ttu-id="9f1f5-163">개발자 팀에 작업 일정 집합 toostop 모든 hello Vm hello 하루 중 특정 시간에을 자동으로 다시 시작을 하루 뒤 hello을 쉽게 매핑할 수 있습니다 하는 설정 자동 종료 및 정책에 의해 자동으로 시작 hello 랩에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f1f5-163">If your developer team has a set work schedule and you want toostop all hello VMs at a particular time of hello day and then automatically restart them hello following day, you can easily accomplish that by setting auto-shutdown and auto-start policies in hello lab.</span></span> 
   
    <span data-ttu-id="9f1f5-164">마지막으로, 앱 개발이 완료 되 면 여 삭제할 수 있습니다 모든 hello Vm을 한 번에 단일 PowerShell 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f1f5-164">Finally, when app development is complete, you can delete all hello VMs at once by running a single PowerShell script.</span></span> 
   
    <span data-ttu-id="9f1f5-165">다음 표에 hello의 hello 링크를 클릭 하 여 자세한 정보:</span><span class="sxs-lookup"><span data-stu-id="9f1f5-165">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="9f1f5-166">작업</span><span class="sxs-lookup"><span data-stu-id="9f1f5-166">Task</span></span> | <span data-ttu-id="9f1f5-167">학습 내용</span><span class="sxs-lookup"><span data-stu-id="9f1f5-167">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="9f1f5-168">랩 정책 정의</span><span class="sxs-lookup"><span data-stu-id="9f1f5-168">Define lab policies</span></span>](devtest-lab-set-lab-policy.md) |<span data-ttu-id="9f1f5-169">Hello 랩에서 정책을 설정 하 여 비용을 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f1f5-169">Control costs by setting policies in hello lab.</span></span> |
   | [<span data-ttu-id="9f1f5-170">모든 hello 랩 PowerShell 스크립트를 사용 하 여 Vm을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f1f5-170">Delete all hello lab VMs using a PowerShell script</span></span>](devtest-lab-faq.md#how-can-i-automate-the-process-of-deleting-all-the-vms-in-my-lab) |<span data-ttu-id="9f1f5-171">개발이 완료 되 면 한 번에 모든 hello labs를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f1f5-171">Delete all hello labs in one operation when development is complete.</span></span>|

1. <span data-ttu-id="9f1f5-172">**가상 네트워크 tooa VM 추가**</span><span class="sxs-lookup"><span data-stu-id="9f1f5-172">**Add a virtual network tooa VM**</span></span> 
   
    <span data-ttu-id="9f1f5-173">DevTest Labs는 랩이 생성될 때마다 새 VNET(가상 네트워크)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9f1f5-173">DevTest Labs creates a new virtual network (VNET) whenever a lab is created.</span></span> <span data-ttu-id="9f1f5-174">-예를 들어 사이트 간 VPN 또는 express 경로 사용 하는 – 여 사용자 고유의 VNET을 구성한 경우에 Vm을 만들 때 사용할 수 있도록이 VNET tooyour 랩의 가상 네트워크 설정을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f1f5-174">If you have configured your own VNET – for example, by using ExpressRoute or site-to-site VPN – you can add this VNET tooyour lab's virtual network settings so that it is available when creating VMs.</span></span>

    <span data-ttu-id="9f1f5-175">또한 Azure Active Directory 도메인 가입 아티팩트 hello VM이 생성 될 때 VM tooa 도메인에 가입 됩니다는 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f1f5-175">In addition, there is an Azure Active Directory domain join artifact available that will join a VM tooa domain when hello VM is being created.</span></span> 
   
    <span data-ttu-id="9f1f5-176">다음 표에 hello의 hello 링크를 클릭 하 여 자세한 정보:</span><span class="sxs-lookup"><span data-stu-id="9f1f5-176">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="9f1f5-177">작업</span><span class="sxs-lookup"><span data-stu-id="9f1f5-177">Task</span></span> | <span data-ttu-id="9f1f5-178">학습 내용</span><span class="sxs-lookup"><span data-stu-id="9f1f5-178">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="9f1f5-179">Azure DevTest Labs에서 가상 네트워크 구성</span><span class="sxs-lookup"><span data-stu-id="9f1f5-179">Configure a virtual network in Azure DevTest Labs</span></span>](devtest-lab-configure-vnet.md) |<span data-ttu-id="9f1f5-180">Tooconfigure Azure DevTest Labs를 사용 하 여 가상 네트워크를 Azure 포털 hello 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="9f1f5-180">Learn how tooconfigure a virtual network in Azure DevTest Labs using hello Azure portal.</span></span>|

6. <span data-ttu-id="9f1f5-181">**Hello 랩 각 개발자와 공유**</span><span class="sxs-lookup"><span data-stu-id="9f1f5-181">**Share hello lab with each developer**</span></span>
   
    <span data-ttu-id="9f1f5-182">개발자와 공유하는 링크를 사용하여 랩에 직접 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f1f5-182">Labs can be directly accessed using a link that you share with your developers.</span></span> <span data-ttu-id="9f1f5-183">도 있지 않아도 toohave Azure 계정을 보유 하는 [Microsoft 계정](devtest-lab-faq.md#what-is-a-microsoft-account)합니다.</span><span class="sxs-lookup"><span data-stu-id="9f1f5-183">They don't even have toohave an Azure account, as long as they have a [Microsoft account](devtest-lab-faq.md#what-is-a-microsoft-account).</span></span> <span data-ttu-id="9f1f5-184">개발자는 다른 개발자가 만든 VM을 볼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9f1f5-184">Developers cannot see VMs created by other developers.</span></span>  
   
    <span data-ttu-id="9f1f5-185">다음 표에 hello의 hello 링크를 클릭 하 여 자세한 정보:</span><span class="sxs-lookup"><span data-stu-id="9f1f5-185">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="9f1f5-186">작업</span><span class="sxs-lookup"><span data-stu-id="9f1f5-186">Task</span></span> | <span data-ttu-id="9f1f5-187">학습 내용</span><span class="sxs-lookup"><span data-stu-id="9f1f5-187">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="9f1f5-188">개발자 tooa 랩 Azure DevTest Labs에 추가</span><span class="sxs-lookup"><span data-stu-id="9f1f5-188">Add a developer tooa lab in Azure DevTest Labs</span></span>](devtest-lab-add-devtest-user.md) |<span data-ttu-id="9f1f5-189">Azure 포털 tooadd 개발자 tooyour 랩 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f1f5-189">Use hello Azure portal tooadd developers tooyour lab.</span></span>|
   | [<span data-ttu-id="9f1f5-190">PowerShell 스크립트를 사용 하 여 개발자가 toohello 랩을 추가합니다</span><span class="sxs-lookup"><span data-stu-id="9f1f5-190">Add developers toohello lab using a PowerShell script</span></span>](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell) |<span data-ttu-id="9f1f5-191">PowerShell tooautomate 개발자 tooyour 랩 추가 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f1f5-191">Use PowerShell tooautomate adding developers tooyour lab.</span></span> |
   | [<span data-ttu-id="9f1f5-192">링크 toohello 랩 가져오기</span><span class="sxs-lookup"><span data-stu-id="9f1f5-192">Get a link toohello lab</span></span>](devtest-lab-faq.md#how-do-i-share-a-direct-link-to-my-lab) |<span data-ttu-id="9f1f5-193">개발자가 하이퍼링크를 통해 랩에 직접 액세스하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="9f1f5-193">Learn how developers can directly access a lab via a hyperlink.</span></span>|

7. <span data-ttu-id="9f1f5-194">**추가 팀을 위한 랩 생성 자동화**</span><span class="sxs-lookup"><span data-stu-id="9f1f5-194">**Automate lab creation for more teams**</span></span> 
   
    <span data-ttu-id="9f1f5-195">사용자 지정 설정을 포함 하 여 리소스 관리자 템플릿을 만들어 사용 하 여 동일한 랩 toocreate 나중에 다시 랩 만들기를 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f1f5-195">You can automate lab creation, including custom settings, by creating a Resource Manager template and using it toocreate identical labs again and again.</span></span> 
   
    <span data-ttu-id="9f1f5-196">다음 표에 hello의 hello 링크를 클릭 하 여 자세한 정보:</span><span class="sxs-lookup"><span data-stu-id="9f1f5-196">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="9f1f5-197">작업</span><span class="sxs-lookup"><span data-stu-id="9f1f5-197">Task</span></span> | <span data-ttu-id="9f1f5-198">학습 내용</span><span class="sxs-lookup"><span data-stu-id="9f1f5-198">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="9f1f5-199">Resource Manager 템플릿을 사용하여 랩 만들기</span><span class="sxs-lookup"><span data-stu-id="9f1f5-199">Create a lab using a Resource Manager template</span></span>](devtest-lab-faq.md#how-do-i-create-a-lab-from-an-azure-resource-manager-template) |<span data-ttu-id="9f1f5-200">Resource Manager 템플릿을 사용하여 Azure DevTest Labs에서 랩을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9f1f5-200">Create labs in Azure DevTest Labs using Resource Manager templates.</span></span> |

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

