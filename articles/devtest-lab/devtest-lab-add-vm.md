---
title: "Azure DevTest Labs에서 랩에 VM 추가 | Microsoft Docs"
description: "Azure DevTest Labs에서 랩에 가상 컴퓨터를 추가하는 방법 알아보기"
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
ms.date: 02/24/2017
ms.author: tarcher
ms.openlocfilehash: 449bffb040dafc8edd0b8b0afd80dbea35cd28ac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="add-a-vm-to-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="da150-103">Azure DevTest Labs에서 랩에 VM 추가</span><span class="sxs-lookup"><span data-stu-id="da150-103">Add a VM to a lab in Azure DevTest Labs</span></span>
<span data-ttu-id="da150-104">[첫 번째 VM을 이미 만든 경우](devtest-lab-create-first-vm.md) 미리 로드된 [Marketplace 이미지](devtest-lab-configure-marketplace-images.md)에서 만들었을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="da150-104">If you have already [created your first VM](devtest-lab-create-first-vm.md), you likely did so from a pre-loaded [marketplace image](devtest-lab-configure-marketplace-images.md).</span></span> <span data-ttu-id="da150-105">이제 이후의 VM을 랩에 추가하려면 [사용자 지정 이미지](devtest-lab-create-template.md) 또는 [수식](devtest-lab-manage-formulas.md)인 *기본*을 선택하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="da150-105">Now, if you want to add subsequent VMs to your lab, you can also choose a *base* that is either a [custom image](devtest-lab-create-template.md) or a [formula](devtest-lab-manage-formulas.md).</span></span> <span data-ttu-id="da150-106">이 자습서에서는 DevTest Labs에서 랩에 VM을 추가하기 위해 Azure Portal을 사용하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="da150-106">This tutorial walks you through using the Azure portal to add a VM to a lab in DevTest Labs.</span></span>

<span data-ttu-id="da150-107">또한 이 문서에서는 랩에서 VM의 아티팩트를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="da150-107">This article also shows you how to manage the artifacts for a VM in your lab.</span></span>

## <a name="steps-to-add-a-vm-to-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="da150-108">Azure DevTest Labs에서 랩에 VM을 추가하는 단계</span><span class="sxs-lookup"><span data-stu-id="da150-108">Steps to add a VM to a lab in Azure DevTest Labs</span></span>
1. <span data-ttu-id="da150-109">[Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="da150-109">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="da150-110">**추가 서비스**를 선택한 후 목록에서 **DevTest Labs**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="da150-110">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
1. <span data-ttu-id="da150-111">랩 목록에서 VM을 만들려는 랩을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="da150-111">From the list of labs, select the lab in which you want to create the VM.</span></span>  
1. <span data-ttu-id="da150-112">랩의 **개요** 블레이드에서 **+ 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="da150-112">On the lab's **Overview** blade, select **+ Add**.</span></span>  

    ![VM 단추 추가](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. <span data-ttu-id="da150-114">**기본 선택** 블레이드에서 VM의 기본을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="da150-114">On the **Choose a base** blade, select a base for the VM.</span></span>
1. <span data-ttu-id="da150-115">**가상 컴퓨터** 블레이드의 **가상 컴퓨터 이름** 텍스트 상자에 새 가상 컴퓨터의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="da150-115">On the **Virtual machine** blade, enter a name for the new virtual machine in the **Virtual machine name** text box.</span></span>

    ![랩 VM 블레이드](./media/devtest-lab-add-vm/devtestlab-lab-vm-blade.png)

1. <span data-ttu-id="da150-117">가상 컴퓨터에서 관리자 권한이 부여된 **사용자 이름**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="da150-117">Enter a **User Name** that is granted administrator privileges on the virtual machine.</span></span>  
1. <span data-ttu-id="da150-118">[비밀 저장소](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store)에 저장된 암호를 사용하려는 경우 **저장된 비밀 사용**을 선택하고 비밀(암호)에 해당하는 키 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="da150-118">If you want to use a password stored in your [secret store](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store), select **Use a saved secret**, and specify a key value that corresponds to your secret (password).</span></span> <span data-ttu-id="da150-119">그렇지 않으면 **값 입력** 텍스트 필드에 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="da150-119">Otherwise, enter a password in the text field labeled **Type a value**.</span></span>
1. <span data-ttu-id="da150-120">**가상 컴퓨터 디스크 유형**은 랩에서 가상 컴퓨터의 저장소 디스크 유형을 허용하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="da150-120">The **Virtual machine disk type** determines which storage disk type is allowed for the virtual machines in the lab.</span></span>
1. <span data-ttu-id="da150-121">**가상 컴퓨터 크기** 를 선택하고 만들려는 프로세서 코어, RAM 크기 및 VM의 하드 드라이브 크기를 지정하는 미리 정의된 항목 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="da150-121">Select **Virtual machine size** and select one of the predefined items that specify the processor cores, RAM size, and the hard drive size of the VM to create.</span></span>
1. <span data-ttu-id="da150-122">**아티팩트** 를 선택하고 아티팩트 목록에서 기본 이미지에 추가하려는 아티팩트를 선택하고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="da150-122">Select **Artifacts** and - from the list of artifacts - select and configure the artifacts that you want to add to the base image.</span></span>
    <span data-ttu-id="da150-123">**참고:** DevTest Lab을 처음 접하거나 아티팩트를 구성 중인 경우 [VM에 기존 아티팩트 추가](#add-an-existing-artifact-to-a-vm) 섹션을 참조한 다음 완료되면 여기로 돌아옵니다.</span><span class="sxs-lookup"><span data-stu-id="da150-123">**Note:** If you're new to DevTest Labs or configuring artifacts, refer to the [Add an existing artifact to a VM](#add-an-existing-artifact-to-a-vm) section, and then return here when finished.</span></span>
1. <span data-ttu-id="da150-124">**고급 설정**을 선택하여 VM의 네트워크 옵션 및 만료 옵션을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="da150-124">Select **Advanced settings** to configure the VM's network options and expiration options.</span></span> 

   <span data-ttu-id="da150-125">만료 옵션을 설정하려면 달력 아이콘을 선택하고 VM이 자동으로 삭제될 날짜를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="da150-125">To set an expiration option, choose the calendar icon to specify a date on which the VM will be automatically deleted.</span></span>  <span data-ttu-id="da150-126">기본적으로 VM은 만료되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="da150-126">By default, the VM will never expire.</span></span> 
1. <span data-ttu-id="da150-127">Azure Resource Manager 템플릿을 보거나 복사하려면 [Azure Resource Manager 템플릿 저장](#save-azure-resource-manager-template) 섹션을 참조하여 원하는 작업을 마친 후에 여기로 다시 돌아옵니다.</span><span class="sxs-lookup"><span data-stu-id="da150-127">If you want to view or copy the Azure Resource Manager template, refer to the [Save Azure Resource Manager template](#save-azure-resource-manager-template) section, and return here when finished.</span></span>
1. <span data-ttu-id="da150-128">**만들기** 를 누르고 지정된 VM을 랩에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="da150-128">Select **Create** to add the specified VM to the lab.</span></span>
1. <span data-ttu-id="da150-129">랩 블레이드는 VM의 만들기 상태를 표시합니다. 처음에는 **생성 중**이 표시되고 VM이 시작하면 **실행 중**으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="da150-129">The lab blade displays the status of the VM's creation - first as **Creating**, then as **Running** after the VM has been started.</span></span>

> [!NOTE]
> <span data-ttu-id="da150-130">[클레임할 수 있는 VM 추가](devtest-lab-add-claimable-vm.md)는 랩에서 모든 사용자가 사용할 수 있도록 VM을 클레임할 수 있게 만드는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="da150-130">[Add a claimable VM](devtest-lab-add-claimable-vm.md) shows you how to make the VM claimable so that it is available for use by any user in the lab.</span></span>
>
>

## <a name="add-an-existing-artifact-to-a-vm"></a><span data-ttu-id="da150-131">VM에 기존 아티팩트 추가</span><span class="sxs-lookup"><span data-stu-id="da150-131">Add an existing artifact to a VM</span></span>
<span data-ttu-id="da150-132">VM을 만드는 동안 기존 아티팩트를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da150-132">While creating a VM, you can add existing artifacts.</span></span> <span data-ttu-id="da150-133">각 랩에는 공용 DevTest Lab 아티팩트 리포지토리의 아티팩트 및 사용자가 만들어서 사용자 고유 아티팩트 리포지토리에 추가한 아티팩트가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da150-133">Each lab includes artifacts from the Public DevTest Labs Artifact Repository as well as artifacts that you've created and added to your own Artifact Repository.</span></span>

* <span data-ttu-id="da150-134">Windows PowerShell 스크립트 실행, Bash 명령 실행 및 소프트웨어 설치 등 Azure DevTest Labs *아티팩트*를 통해 VM을 프로비전할 때 수행하는 *작업*을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da150-134">Azure DevTest Labs *artifacts* let you specify *actions* that are performed when the VM is provisioned, such as running Windows PowerShell scripts, running Bash commands, and installing software.</span></span>
* <span data-ttu-id="da150-135">아티팩트 *매개 변수*를 통해 특정 시나리오에 대한 아티팩트를 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da150-135">Artifact *parameters* let you customize the artifact for your particular scenario</span></span>

<span data-ttu-id="da150-136">아티팩트를 만드는 방법을 알아보려면 [DevTest Labs와 함께 사용할 사용자 고유의 아티팩트를 저작하는 방법 알아보기](devtest-lab-artifact-author.md)문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da150-136">To discover how to create artifacts, see the article, [Learn how to author your own artifacts for use with DevTest Labs](devtest-lab-artifact-author.md).</span></span>

1. <span data-ttu-id="da150-137">[Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="da150-137">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="da150-138">**추가 서비스**를 선택한 후 목록에서 **DevTest Labs**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="da150-138">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
1. <span data-ttu-id="da150-139">랩 목록에서 사용하려는 VM을 포함하는 랩을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="da150-139">From the list of labs, select the lab containing the VM with which you want to work.</span></span>  
1. <span data-ttu-id="da150-140">**내 가상 컴퓨터**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="da150-140">Select **My virtual machines**.</span></span>
1. <span data-ttu-id="da150-141">원하는 VM을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="da150-141">Select the desired VM.</span></span>
1. <span data-ttu-id="da150-142">**아티팩트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="da150-142">Select **Artifacts**.</span></span> 
1. <span data-ttu-id="da150-143">**아티팩트 적용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="da150-143">Select **Apply artifacts**.</span></span>
1. <span data-ttu-id="da150-144">**아티팩트 적용** 블레이드에서 VM에 추가하려는 아티팩트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="da150-144">On the **Apply artifacts** blade, select the artifact you wish to add to the VM.</span></span>
1. <span data-ttu-id="da150-145">**아티팩트 추가** 블레이드에서 필수 매개 변수 값 및 필요한 선택적 매개 변수를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="da150-145">On the **Add artifact** blade, enter the required parameter values and any optional parameters that you need.</span></span>  
1. <span data-ttu-id="da150-146">**추가**를 선택하여 아티팩트를 추가하고 **아티팩트 적용** 블레이드로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="da150-146">Select **Add** to add the artifact and return to the **Apply artifacts** blade.</span></span>
1. <span data-ttu-id="da150-147">VM에 필요한 만큼 계속해서 아티팩트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="da150-147">Continue adding artifacts as needed for your VM.</span></span>
1. <span data-ttu-id="da150-148">아티팩트를 추가한 후에는 [아티팩트가 실행되는 순서를 변경](#change-the-order-in-which-artifacts-are-run)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da150-148">Once you've added your artifacts, you can [change the order in which the artifacts are run](#change-the-order-in-which-artifacts-are-run).</span></span> <span data-ttu-id="da150-149">뒤로 돌아가서 [아티팩트를 확인 또는 수정](#view-or-modify-an-artifact)할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da150-149">You can also go back to [view or modify an artifact](#view-or-modify-an-artifact).</span></span>
1. <span data-ttu-id="da150-150">아티팩트 추가를 마친 경우 **적용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="da150-150">When you're done adding artifacts, select **Apply**</span></span>

## <a name="change-the-order-in-which-artifacts-are-run"></a><span data-ttu-id="da150-151">아티팩트가 실행되는 순서 변경</span><span class="sxs-lookup"><span data-stu-id="da150-151">Change the order in which artifacts are run</span></span>
<span data-ttu-id="da150-152">기본적으로 아티팩트 작업은 VM에 추가된 순서로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="da150-152">By default, the actions of the artifacts are executed in the order in which they are added to the VM.</span></span> <span data-ttu-id="da150-153">다음 단계에서는 아티팩트가 실행되는 순서를 변경하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="da150-153">The following steps illustrate how to change the order in which the artifacts are run.</span></span>

1. <span data-ttu-id="da150-154">**아티팩트 적용** 블레이드의 맨 위에서 VM에 추가된 아티팩트 수를 나타내는 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="da150-154">At the top of the **Apply artifacts** blade, select the link indicating the number of artifacts that have been added to the VM.</span></span>
   
    ![VM에 추가된 아티팩트의 수](./media/devtest-lab-add-vm-with-artifacts/devtestlab-add-artifacts-blade-selected-artifacts.png)
1. <span data-ttu-id="da150-156">**선택한 아티팩트** 블레이드에서 아티팩트를 원하는 순서로 끌어다 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="da150-156">On the **Selected artifacts** blade, drag and drop the artifacts into the desired order.</span></span> <span data-ttu-id="da150-157">**참고:** 아티팩트를 끌어 놓는 데 문제가 있으면 아티팩트의 왼쪽에서 끌어 놓으세요.</span><span class="sxs-lookup"><span data-stu-id="da150-157">**Note:** If you have trouble dragging the artifact, make sure that you are dragging from the left side of the artifact.</span></span> 
1. <span data-ttu-id="da150-158">완료되면 **확인** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="da150-158">Select **OK** when done.</span></span>  

## <a name="view-or-modify-an-artifact"></a><span data-ttu-id="da150-159">아티팩트를 확인 또는 수정</span><span class="sxs-lookup"><span data-stu-id="da150-159">View or modify an artifact</span></span>
<span data-ttu-id="da150-160">다음 단계에서는 아티팩트의 매개 변수를 확인 또는 수정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="da150-160">The following steps illustrate how to view or modify the parameters of an artifact:</span></span>

1. <span data-ttu-id="da150-161">**아티팩트 적용** 블레이드의 맨 위에서 VM에 추가된 아티팩트 수를 나타내는 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="da150-161">At the top of the **Apply artifacts** blade, select the link indicating the number of artifacts that have been added to the VM.</span></span>
   
    ![VM에 추가된 아티팩트의 수](./media/devtest-lab-add-vm-with-artifacts/devtestlab-add-artifacts-blade-selected-artifacts.png)
1. <span data-ttu-id="da150-163">**선택한 아티팩트** 블레이드에서 확인 또는 편집하려는 아티팩트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="da150-163">On the **Selected artifacts** blade, select the artifact that you want to view or edit.</span></span>  
1. <span data-ttu-id="da150-164">**아티팩트 추가** 블레이드에서 필요한 부분을 변경하고 **확인**을 선택하여 **아티팩트 추가** 블레이드를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="da150-164">On the **Add artifact** blade, make any needed changes, and select **OK** to close the **Add artifact** blade.</span></span>
1. <span data-ttu-id="da150-165">**확인**을 선택하여 **선택한 아티팩트** 블레이드를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="da150-165">Select **OK** to close the **Selected artifacts** blade.</span></span>

## <a name="save-azure-resource-manager-template"></a><span data-ttu-id="da150-166">Azure Resource Manager 템플릿 저장</span><span class="sxs-lookup"><span data-stu-id="da150-166">Save Azure Resource Manager template</span></span>
<span data-ttu-id="da150-167">Azure Resource Manager 템플릿을 사용하면 반복 가능한 배포를 선언적으로 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da150-167">An Azure Resource Manager template provides a declarative way to define a repeatable deployment.</span></span> <span data-ttu-id="da150-168">다음 단계는 생성 중인 VM에 대한 Azure Resource Manager 템플릿을 저장하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="da150-168">The following steps explain how to save the Azure Resource Manager template for the VM being created.</span></span>
<span data-ttu-id="da150-169">저장한 Azure Resource Manager 템플릿은 [Azure PowerShell로 새 VM을 배포](../azure-resource-manager/resource-group-overview.md#template-deployment)하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da150-169">Once saved, you can use the Azure Resource Manager template to [deploy new VMs with Azure PowerShell](../azure-resource-manager/resource-group-overview.md#template-deployment).</span></span>

1. <span data-ttu-id="da150-170">**가상 컴퓨터** 블레이드에서 **ARM 템플릿 보기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="da150-170">On the **Virtual machine** blade, select **View ARM Template**.</span></span>
2. <span data-ttu-id="da150-171">**Azure Resource Manager 템플릿 보기** 블레이드에서 템플릿 텍스트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="da150-171">On the **View Azure Resource Manager template** blade, select the template text.</span></span>
3. <span data-ttu-id="da150-172">선택한 텍스트를 클립보드에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="da150-172">Copy the selected text to the clipboard.</span></span>
4. <span data-ttu-id="da150-173">**확인**을 선택하여 **Azure Resource Manager 템플릿 블레이드 보기**를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="da150-173">Select **OK** to close the **View Azure Resource Manager Template blade**.</span></span>
5. <span data-ttu-id="da150-174">텍스트 편집기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="da150-174">Open a text editor.</span></span>
6. <span data-ttu-id="da150-175">클립보드의 템플릿 텍스트를 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="da150-175">Paste in the template text from the clipboard.</span></span>
7. <span data-ttu-id="da150-176">나중에 사용할 수 있도록 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="da150-176">Save the file for later use.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

### <a name="next-steps"></a><span data-ttu-id="da150-177">다음 단계</span><span class="sxs-lookup"><span data-stu-id="da150-177">Next steps</span></span>
* <span data-ttu-id="da150-178">VM을 만든 후에는 해당 VM의 블레이드에서 **연결** 을 선택하여 VM에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da150-178">Once the VM has been created, you can connect to the VM by selecting **Connect** on the VM's blade.</span></span>
* <span data-ttu-id="da150-179">[DevTest Labs VM용 사용자 지정 아티팩트 작성](devtest-lab-artifact-author.md)방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="da150-179">Learn how to [create custom artifacts for your DevTest Labs VM](devtest-lab-artifact-author.md).</span></span>
* <span data-ttu-id="da150-180">[DevTest Labs Azure Resource Manager 빠른 시작 템플릿 갤러리](https://github.com/Azure/azure-devtestlab/tree/master/Samples)를 탐색합니다.</span><span class="sxs-lookup"><span data-stu-id="da150-180">Explore the [DevTest Labs Azure Resource Manager QuickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/Samples).</span></span>
