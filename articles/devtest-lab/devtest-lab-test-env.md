---
title: "VM 및 PaaS aaaUse Azure DevTest Labs 테스트 환경 | Microsoft Docs"
description: "VM 및 PaaS toouse Azure DevTest Labs 환경 시나리오를 테스트 하는 방법에 대해 알아봅니다."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: d4e2c334-643a-40c9-9051-625b8f39fc86
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: tarcher
ms.openlocfilehash: 9285090da768491e1275942318b094fae89e3273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-devtest-labs-for-vm-and-paas-test-environments"></a><span data-ttu-id="7372a-103">VM 및 PaaS 테스트 환경에 Azure DevTest Labs 사용</span><span class="sxs-lookup"><span data-stu-id="7372a-103">Use Azure DevTest Labs for VM and PaaS test environments</span></span>

<span data-ttu-id="7372a-104">Azure DevTest Labs tooimplement 여러 주요 시나리오를 사용할 수 있습니다 하지만 기본 시나리오에서는 DevTest Labs toohost 컴퓨터를 사용 하 여 테스터에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="7372a-104">You can use Azure DevTest Labs tooimplement many key scenarios, but a primary scenario involves using DevTest Labs toohost machines for testers.</span></span> 

<span data-ttu-id="7372a-105">이 시나리오에서 DevTest Labs는 다음과 같은 이점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7372a-105">In this scenario, DevTest Labs provides these benefits:</span></span>

- <span data-ttu-id="7372a-106">테스터 신속 하 게 다시 사용할 수 있는 템플릿 및 아티팩트를 사용 하 여 Windows 및 Linux 환경 프로 비전 하 여 hello 응용 프로그램의 최신 버전을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7372a-106">Testers can test hello latest version of their application by quickly provisioning Windows and Linux environments using reusable templates and artifacts.</span></span>
- <span data-ttu-id="7372a-107">테스터가 다수의 테스트 에이전트를 프로비전하여 부하 테스트를 강화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7372a-107">Testers can scale up their load testing by provisioning multiple test agents.</span></span>
- <span data-ttu-id="7372a-108">관리자는 다음을 확인하여 비용을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7372a-108">Administrators can control costs by ensuring that:</span></span>
  - <span data-ttu-id="7372a-109">테스터는 VM을 필요 이상으로 가질 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7372a-109">Testers cannot get more VMs than they need.</span></span>
  - <span data-ttu-id="7372a-110">VM은 사용되지 않을 때 종료됩니다.</span><span class="sxs-lookup"><span data-stu-id="7372a-110">VMs are shut down when not in use.</span></span>

![학습에 DevTest Labs 사용](./media/devtest-lab-developer-lab/devtest-lab-developer-lab.png)

<span data-ttu-id="7372a-112">이 문서에서는 다양 한 Azure DevTest Labs 사용 되는 기능 toomeet 테스터 요구 사항 및 자세한 단계 toofollow tooset 랩을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="7372a-112">In this article, you learn about various Azure DevTest Labs features used toomeet tester requirements and hello detailed steps toofollow tooset up a lab.</span></span>

## <a name="implementing-test-environments-with-azure-devtest-labs"></a><span data-ttu-id="7372a-113">Azure DevTest Labs를 사용하여 테스트 환경 구현</span><span class="sxs-lookup"><span data-stu-id="7372a-113">Implementing test environments with Azure DevTest Labs</span></span>
1. <span data-ttu-id="7372a-114">**Hello 랩 만들기**</span><span class="sxs-lookup"><span data-stu-id="7372a-114">**Create hello lab**</span></span> 
   
    <span data-ttu-id="7372a-115">랩은 hello Azure DevTest Labs의 시작 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="7372a-115">Labs are hello starting point in Azure DevTest Labs.</span></span> <span data-ttu-id="7372a-116">랩을 만든 후 사용자 (테스터) toohello 랩, 설정 정책 toocontrol 비용을 신속 하 게 만들 수 있는 VM 이미지를 정의 및 추가 같은 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7372a-116">Once you create a lab, you can perform tasks such as adding users (testers) toohello lab, setting policies toocontrol costs, defining VM images that can create quickly, and more.</span></span>  
   
    <span data-ttu-id="7372a-117">다음 표에 hello의 hello 링크를 클릭 하 여 자세한 정보:</span><span class="sxs-lookup"><span data-stu-id="7372a-117">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="7372a-118">작업</span><span class="sxs-lookup"><span data-stu-id="7372a-118">Task</span></span> | <span data-ttu-id="7372a-119">학습 내용</span><span class="sxs-lookup"><span data-stu-id="7372a-119">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="7372a-120">Azure DevTest Labs에서 랩 만들기</span><span class="sxs-lookup"><span data-stu-id="7372a-120">Create a lab in Azure DevTest Labs</span></span>](devtest-lab-create-lab.md) |<span data-ttu-id="7372a-121">Toocreate 랩에서 DevTest Labs를 Azure에는 Azure 포털 hello 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7372a-121">Learn how toocreate a lab in Azure DevTest Labs in hello Azure portal.</span></span> |
2. <span data-ttu-id="7372a-122">**바로 사용할 수 있는 마켓플레이스 이미지 및 사용자 지정 이미지를 사용하여 몇 분 만에 VM 만들기**</span><span class="sxs-lookup"><span data-stu-id="7372a-122">**Create VMs in minutes using ready-made marketplace images and custom images**</span></span> 
   
    <span data-ttu-id="7372a-123">Hello Azure Marketplace에서에서 다양 한 이미지에서에서 즉시 사용 가능한 이미지를 선택 하 고 hello 랩에서 사용할 수 있도록 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7372a-123">You can pick ready-made images from a wide variety of images in hello Azure Marketplace and make them available in hello lab.</span></span> <span data-ttu-id="7372a-124">Hello 즉시 사용 가능한 이미지 요구 사항을 충족 하지 않는 경우에 랩 hello 랩에 대 한 사용자 지정 이미지로 Azure 마켓플레이스를 필요한 모든 hello 소프트웨어를 설치 하 고 저장 하는 hello VM에서 이미 만들어진 이미지를 사용 하 여 VM을 만들어 사용자 지정 이미지를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7372a-124">If hello ready-made images don't meet your requirements, you can create a custom image by creating a lab VM using a ready-made image from Azure Marketplace, installing all hello software that you need, and saving hello VM as a custom image in hello lab.</span></span>

    <span data-ttu-id="7372a-125">사용자 지정 이미지를 사용 하는 경우 이미지 팩터리 toocreate를 사용 하 여 분산 하 여 이미지 합니다.</span><span class="sxs-lookup"><span data-stu-id="7372a-125">If you will be using custom images, consider using an image factory toocreate and distribute your images.</span></span> <span data-ttu-id="7372a-126">이미지 팩터리는 구성된 이미지를 자동으로 정기적으로 작성 및 배포하는 "코드로 구성" 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="7372a-126">An image factory is a configuration-as-code solution that regularly builds and distributes your configured images automatically.</span></span> <span data-ttu-id="7372a-127">이 저장 hello 필요한 시간 toomanually hello로 VM이 만들어진 후 hello 시스템 구성 운영 체제를 기반 합니다.</span><span class="sxs-lookup"><span data-stu-id="7372a-127">This saves hello time required toomanually configure hello system after a VM has been created with hello base OS.</span></span>
  
    <span data-ttu-id="7372a-128">다음 표에 hello의 hello 링크를 클릭 하 여 자세한 정보:</span><span class="sxs-lookup"><span data-stu-id="7372a-128">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="7372a-129">작업</span><span class="sxs-lookup"><span data-stu-id="7372a-129">Task</span></span> | <span data-ttu-id="7372a-130">학습 내용</span><span class="sxs-lookup"><span data-stu-id="7372a-130">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="7372a-131">Azure Marketplace 이미지 구성</span><span class="sxs-lookup"><span data-stu-id="7372a-131">Configure Azure Marketplace images</span></span>](devtest-lab-configure-marketplace-images.md) |<span data-ttu-id="7372a-132">방법을 알아봅니다 화이트 리스트 Azure 마켓플레이스 이미지 hello 테스터에 대해 원하는 선택만 hello 이미지를 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7372a-132">Learn how you can whitelist Azure Marketplace images, making available for selection only hello images you want for hello testers.</span></span>|
   | [<span data-ttu-id="7372a-133">사용자 지정 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="7372a-133">Create a custom image</span></span>](devtest-lab-create-template.md) |<span data-ttu-id="7372a-134">사전 테스터 hello 사용자 지정 이미지를 사용 하는 VM을 신속 하 게 만들 수 있도록 해야 하는 hello 소프트웨어를 설치 하 여 사용자 지정 이미지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7372a-134">Create a custom image by pre-installing hello software you need so that testers can quickly create a VM using hello custom image.</span></span>|
   | [<span data-ttu-id="7372a-135">이미지 팩터리에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="7372a-135">Learn about image factory</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2017/04/17/video-custom-image-factory-with-azure-devtest-labs/) |<span data-ttu-id="7372a-136">설명 하는 비디오를 시청 방법을 tooset 및 이미지 팩터리를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7372a-136">Watch a video that describes how tooset up and use an image factory.</span></span>|

3. <span data-ttu-id="7372a-137">**테스트 컴퓨터에 재사용 가능한 템플릿 만들기**</span><span class="sxs-lookup"><span data-stu-id="7372a-137">**Create reusable templates for test machines**</span></span> 
   
    <span data-ttu-id="7372a-138">Azure DevTest Labs의 수식에서는 toocreate VM을 사용 하는 기본 속성 값의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="7372a-138">A formula in Azure DevTest Labs is a list of default property values used toocreate a VM.</span></span> <span data-ttu-id="7372a-139">이미지, VM 크기 (CPU 및 RAM의 조합), 및 가상 네트워크를 선택 하 여 hello 랩에서 수식을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7372a-139">You can create a formula in hello lab by picking an image, a VM size (a combination of CPU and RAM), and a virtual network.</span></span> <span data-ttu-id="7372a-140">각 테스터 hello 랩에서 hello 수식을 보고 toocreate VM을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7372a-140">Each tester can see hello formula in hello lab and use it toocreate a VM.</span></span> 
   
    <span data-ttu-id="7372a-141">다음 표에 hello의 hello 링크를 클릭 하 여 자세한 정보:</span><span class="sxs-lookup"><span data-stu-id="7372a-141">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="7372a-142">작업</span><span class="sxs-lookup"><span data-stu-id="7372a-142">Task</span></span> | <span data-ttu-id="7372a-143">학습 내용</span><span class="sxs-lookup"><span data-stu-id="7372a-143">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="7372a-144">DevTest Labs 수식 toocreate Vm 관리</span><span class="sxs-lookup"><span data-stu-id="7372a-144">Manage DevTest Labs formulas toocreate VMs</span></span>](devtest-lab-manage-formulas.md) |<span data-ttu-id="7372a-145">이미지, VM 크기(CPU와 RAM의 조합) 및 가상 네트워크를 선택하여 수식을 만들 수 있는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7372a-145">Learn how you can create a formula by picking up an image, VM size (combination of CPU and RAM), and a virtual network.</span></span>|

3. <span data-ttu-id="7372a-146">**다중 VM 테스트 환경 만들기**</span><span class="sxs-lookup"><span data-stu-id="7372a-146">**Create multi-VM test environments**</span></span> 
   
    <span data-ttu-id="7372a-147">Azure 리소스 관리자 템플릿 toodefine hello 인프라 및 Azure 솔루션의 구성을 사용할 수 있으며 여러 테스트 Vm 일관 된 상태에서 반복적으로 배포 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7372a-147">You can use Azure Resource Manager templates toodefine hello infrastructure and configuration of your Azure solution and repeatedly deploy multiple test VMs in a consistent state.</span></span>

    <span data-ttu-id="7372a-148">Azure PaaS 리소스는 Resource Manager 템플릿의 환경에서 프로비전할 수 있고 비용 추적에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7372a-148">Azure PaaS resources can be provisioned in an environment from a Resource Manager template and appear in cost tracking.</span></span> <span data-ttu-id="7372a-149">그러나 VM 자동 종료 tooPaaS 리소스 적용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7372a-149">However, VM auto shutdown does not apply tooPaaS resources.</span></span>

    <span data-ttu-id="7372a-150">다음 표에 hello의 hello 링크를 클릭 하 여 자세한 정보:</span><span class="sxs-lookup"><span data-stu-id="7372a-150">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="7372a-151">작업</span><span class="sxs-lookup"><span data-stu-id="7372a-151">Task</span></span> | <span data-ttu-id="7372a-152">학습 내용</span><span class="sxs-lookup"><span data-stu-id="7372a-152">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="7372a-153">Azure Resource Manager 템플릿으로 다중 VM 환경 및 PaaS 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="7372a-153">Create multi-VM environments and PaaS resources with Azure Resource Manager templates</span></span>](devtest-lab-create-environment-from-arm.md) |<span data-ttu-id="7372a-154">테스트 환경에 일관된 상태로 여러 VM을 배포하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7372a-154">Learn how you can deploy multiple VMs in a consistent state for your test environment.</span></span>|

4. <span data-ttu-id="7372a-155">**아티팩트 tooenable 유연한 VM 사용자 지정 만들기**</span><span class="sxs-lookup"><span data-stu-id="7372a-155">**Create artifacts tooenable flexible VM customization**</span></span>

   <span data-ttu-id="7372a-156">아티팩트는 사용 되는 toodeploy 및 VM 프로 비전 된 후 응용 프로그램을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7372a-156">Artifacts are used toodeploy and configure your application after a VM is provisioned.</span></span> <span data-ttu-id="7372a-157">아티팩트는 다음과 같을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7372a-157">Artifacts can be:</span></span>

   - <span data-ttu-id="7372a-158">에이전트, Fiddler 및 Visual Studio와 같은 VM-hello에 tooinstall 원하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="7372a-158">Tools that you want tooinstall on hello VM - such as agents, Fiddler, and Visual Studio.</span></span>
   - <span data-ttu-id="7372a-159">리포지토리 복제 같은 VM-hello에 toorun 되도록 동작입니다.</span><span class="sxs-lookup"><span data-stu-id="7372a-159">Actions that you want toorun on hello VM - such as cloning a repo.</span></span>
   - <span data-ttu-id="7372a-160">응용 프로그램 tootest 한다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7372a-160">Applications that you want tootest.</span></span>

   <span data-ttu-id="7372a-161">많은 아티팩트는 이미 기본 제공되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7372a-161">Many artifacts are already available out-of-the-box.</span></span> <span data-ttu-id="7372a-162">특정 요구에 맞게 추가로 사용자 지정하려는 경우 자시만의 사용자 지정 아티팩트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7372a-162">But if you want more customization for your specific needs, you can create your own custom artifacts.</span></span>

   <span data-ttu-id="7372a-163">다음 표에 hello의 hello 링크를 클릭 하 여 자세한 정보:</span><span class="sxs-lookup"><span data-stu-id="7372a-163">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="7372a-164">작업</span><span class="sxs-lookup"><span data-stu-id="7372a-164">Task</span></span> | <span data-ttu-id="7372a-165">학습 내용</span><span class="sxs-lookup"><span data-stu-id="7372a-165">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="7372a-166">DevTest Lab VM에 대한 사용자 지정 아티팩트 만들기</span><span class="sxs-lookup"><span data-stu-id="7372a-166">Create custom artifacts for your DevTest Labs VM</span></span>](devtest-lab-artifact-author.md) |<span data-ttu-id="7372a-167">랩에서 hello 가상 컴퓨터에 대 한 사용자 고유의 사용자 지정 아티팩트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7372a-167">Create your own custom artifacts for hello virtual machines in your lab.</span></span>|
   | [<span data-ttu-id="7372a-168">Azure DevTest Labs에서 Git 리포지토리 toostore 사용자 지정 아티팩트 및 Azure 리소스 관리자 템플릿을 사용 하기 위해 추가</span><span class="sxs-lookup"><span data-stu-id="7372a-168">Add a Git repository toostore custom artifacts and Azure Resource Manager templates for use in Azure DevTest Labs</span></span>](devtest-lab-add-artifact-repo.md) |<span data-ttu-id="7372a-169">자세한 내용은 방법 toostore 자신의 개인 Git 리포지토리에 있는 사용자 지정 아티팩트입니다.</span><span class="sxs-lookup"><span data-stu-id="7372a-169">Learn how toostore your custom artifacts in your own private Git repo.</span></span>|

5. <span data-ttu-id="7372a-170">**비용 제어**</span><span class="sxs-lookup"><span data-stu-id="7372a-170">**Control costs**</span></span>
   
    <span data-ttu-id="7372a-171">Azure DevTest Labs hello 랩 toospecify hello 최대 Vm 수 hello 랩에서 테스터에 의해 만들어진에 tooset 정책을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7372a-171">Azure DevTest Labs allows you tooset a policy in hello lab toospecify hello maximum number of VMs that can be created by a tester in hello lab.</span></span> 
   
    <span data-ttu-id="7372a-172">테스트 팀에 작업 일정 집합 toostop 모든 hello Vm hello 하루 중 특정 시간에을 자동으로 다시 시작을 하루 뒤 hello을 쉽게 매핑할 수 있습니다 하는 설정 자동 종료 및 정책에 의해 자동으로 시작 hello 랩에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="7372a-172">If your test team has a set work schedule and you want toostop all hello VMs at a particular time of hello day and then automatically restart them hello following day, you can easily accomplish that by setting auto-shutdown and auto-start policies in hello lab.</span></span> 
   
    <span data-ttu-id="7372a-173">마지막으로, 앱 개발이 완료 되 면 여 삭제할 수 있습니다 모든 hello Vm을 한 번에 단일 PowerShell 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7372a-173">Finally, when app development is complete, you can delete all hello VMs at once by running a single PowerShell script.</span></span> 
   
    <span data-ttu-id="7372a-174">다음 표에 hello의 hello 링크를 클릭 하 여 자세한 정보:</span><span class="sxs-lookup"><span data-stu-id="7372a-174">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="7372a-175">작업</span><span class="sxs-lookup"><span data-stu-id="7372a-175">Task</span></span> | <span data-ttu-id="7372a-176">학습 내용</span><span class="sxs-lookup"><span data-stu-id="7372a-176">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="7372a-177">랩 정책 정의</span><span class="sxs-lookup"><span data-stu-id="7372a-177">Define lab policies</span></span>](devtest-lab-set-lab-policy.md) |<span data-ttu-id="7372a-178">Hello 랩에서 정책을 설정 하 여 비용을 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="7372a-178">Control costs by setting policies in hello lab.</span></span> |
   | [<span data-ttu-id="7372a-179">모든 hello 랩 PowerShell 스크립트를 사용 하 여 Vm을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="7372a-179">Delete all hello lab VMs using a PowerShell script</span></span>](devtest-lab-faq.md#how-can-i-automate-the-process-of-deleting-all-the-vms-in-my-lab) |<span data-ttu-id="7372a-180">테스트가 완료 되 면 한 번에 모든 hello labs를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="7372a-180">Delete all hello labs in one operation when testing is complete.</span></span>|

1. <span data-ttu-id="7372a-181">**가상 네트워크 tooa 랩 추가**</span><span class="sxs-lookup"><span data-stu-id="7372a-181">**Add a virtual network tooa Lab**</span></span> 
   
    <span data-ttu-id="7372a-182">DevTest Labs는 랩이 생성될 때마다 새 VNET(가상 네트워크)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7372a-182">DevTest Labs creates a new virtual network (VNET) whenever a lab is created.</span></span> <span data-ttu-id="7372a-183">-예를 들어 사이트 간 VPN 또는 express 경로 사용 하는 – 여 사용자 고유의 VNET을 구성한 경우에 Vm을 만들 때 사용할 수 있도록이 VNET tooyour 랩의 가상 네트워크 설정을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7372a-183">If you have configured your own VNET – for example, by using ExpressRoute or site-to-site VPN – you can add this VNET tooyour lab's virtual network settings so that it is available when creating VMs.</span></span>

    <span data-ttu-id="7372a-184">또한 Azure Active Directory 도메인 가입 아티팩트 사용할 수 있는 hello VM이 생성 될 때 VM tooa 도메인에 가입 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="7372a-184">In addition, there is an Azure Active Directory domain join artifact available that joins a VM tooa domain when hello VM is being created.</span></span> 
   
    <span data-ttu-id="7372a-185">다음 표에 hello의 hello 링크를 클릭 하 여 자세한 정보:</span><span class="sxs-lookup"><span data-stu-id="7372a-185">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="7372a-186">작업</span><span class="sxs-lookup"><span data-stu-id="7372a-186">Task</span></span> | <span data-ttu-id="7372a-187">학습 내용</span><span class="sxs-lookup"><span data-stu-id="7372a-187">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="7372a-188">Azure DevTest Labs에서 가상 네트워크 구성</span><span class="sxs-lookup"><span data-stu-id="7372a-188">Configure a virtual network in Azure DevTest Labs</span></span>](devtest-lab-configure-vnet.md) |<span data-ttu-id="7372a-189">Tooconfigure Azure DevTest Labs를 사용 하 여 가상 네트워크를 Azure 포털 hello 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7372a-189">Learn how tooconfigure a virtual network in Azure DevTest Labs using hello Azure portal.</span></span>|

6. <span data-ttu-id="7372a-190">**각 테스터와 hello 랩 공유**</span><span class="sxs-lookup"><span data-stu-id="7372a-190">**Share hello lab with each tester**</span></span>
   
    <span data-ttu-id="7372a-191">테스터와 공유하는 링크를 사용하여 랩에 직접 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7372a-191">Labs can be directly accessed using a link that you share with your testers.</span></span> <span data-ttu-id="7372a-192">도 있지 않아도 toohave Azure 계정을 보유 하는 [Microsoft 계정](devtest-lab-faq.md#what-is-a-microsoft-account)합니다.</span><span class="sxs-lookup"><span data-stu-id="7372a-192">They don't even have toohave an Azure account, as long as they have a [Microsoft account](devtest-lab-faq.md#what-is-a-microsoft-account).</span></span> <span data-ttu-id="7372a-193">테스터는 다른 테스터가 만든 VM을 볼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7372a-193">Testers cannot see VMs created by other testers.</span></span>  
   
    <span data-ttu-id="7372a-194">다음 표에 hello의 hello 링크를 클릭 하 여 자세한 정보:</span><span class="sxs-lookup"><span data-stu-id="7372a-194">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="7372a-195">작업</span><span class="sxs-lookup"><span data-stu-id="7372a-195">Task</span></span> | <span data-ttu-id="7372a-196">학습 내용</span><span class="sxs-lookup"><span data-stu-id="7372a-196">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="7372a-197">Azure DevTest Labs에서 테스터 tooa 랩 추가</span><span class="sxs-lookup"><span data-stu-id="7372a-197">Add a tester tooa lab in Azure DevTest Labs</span></span>](devtest-lab-add-devtest-user.md) |<span data-ttu-id="7372a-198">Azure 포털 tooadd 테스터 tooyour 랩 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7372a-198">Use hello Azure portal tooadd testers tooyour lab.</span></span>|
   | [<span data-ttu-id="7372a-199">PowerShell 스크립트를 사용 하 여 테스터 toohello 랩을 추가합니다</span><span class="sxs-lookup"><span data-stu-id="7372a-199">Add testers toohello lab using a PowerShell script</span></span>](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell) |<span data-ttu-id="7372a-200">PowerShell tooautomate 테스터 tooyour 랩 추가 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7372a-200">Use PowerShell tooautomate adding testers tooyour lab.</span></span> |
   | [<span data-ttu-id="7372a-201">링크 toohello 랩 가져오기</span><span class="sxs-lookup"><span data-stu-id="7372a-201">Get a link toohello lab</span></span>](devtest-lab-faq.md#how-do-i-share-a-direct-link-to-my-lab) |<span data-ttu-id="7372a-202">테스터가 하이퍼링크를 통해 랩에 직접 액세스하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7372a-202">Learn how testers can directly access a lab via a hyperlink.</span></span>|

7. <span data-ttu-id="7372a-203">**추가 팀을 위한 랩 생성 자동화**</span><span class="sxs-lookup"><span data-stu-id="7372a-203">**Automate lab creation for more teams**</span></span> 
   
    <span data-ttu-id="7372a-204">사용자 지정 설정을 포함 하 여 리소스 관리자 템플릿을 만들어 사용 하 여 동일한 랩 toocreate 나중에 다시 랩 만들기를 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7372a-204">You can automate lab creation, including custom settings, by creating a Resource Manager template and using it toocreate identical labs again and again.</span></span> 
   
    <span data-ttu-id="7372a-205">다음 표에 hello의 hello 링크를 클릭 하 여 자세한 정보:</span><span class="sxs-lookup"><span data-stu-id="7372a-205">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="7372a-206">작업</span><span class="sxs-lookup"><span data-stu-id="7372a-206">Task</span></span> | <span data-ttu-id="7372a-207">학습 내용</span><span class="sxs-lookup"><span data-stu-id="7372a-207">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="7372a-208">Resource Manager 템플릿을 사용하여 랩 만들기</span><span class="sxs-lookup"><span data-stu-id="7372a-208">Create a lab using a Resource Manager template</span></span>](devtest-lab-faq.md#how-do-i-create-a-lab-from-an-azure-resource-manager-template) |<span data-ttu-id="7372a-209">Resource Manager 템플릿을 사용하여 Azure DevTest Labs에서 랩을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7372a-209">Create labs in Azure DevTest Labs using Resource Manager templates.</span></span> |

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

