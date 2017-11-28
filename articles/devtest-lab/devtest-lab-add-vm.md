---
title: "DevTest Labs Azure에서에서 VM tooa 랩 aaaAdd | Microsoft Docs"
description: "자세한 내용은 방법 tooadd DevTest Labs Azure에서에서 가상 컴퓨터 tooa 랩"
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
ms.openlocfilehash: 82838e4349550db56de311264c188140b9556b24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-vm-tooa-lab-in-azure-devtest-labs"></a><span data-ttu-id="3e3dd-103">DevTest Labs Azure에서에서 VM tooa 랩 추가</span><span class="sxs-lookup"><span data-stu-id="3e3dd-103">Add a VM tooa lab in Azure DevTest Labs</span></span>
<span data-ttu-id="3e3dd-104">[첫 번째 VM을 이미 만든 경우](devtest-lab-create-first-vm.md) 미리 로드된 [Marketplace 이미지](devtest-lab-configure-marketplace-images.md)에서 만들었을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3e3dd-104">If you have already [created your first VM](devtest-lab-create-first-vm.md), you likely did so from a pre-loaded [marketplace image](devtest-lab-configure-marketplace-images.md).</span></span> <span data-ttu-id="3e3dd-105">이제 tooadd 후속 Vm tooyour 랩 하려는 경우 선택할 수도 있습니다는 *기본* 즉는 [사용자 지정 이미지](devtest-lab-create-template.md) 또는 [수식](devtest-lab-manage-formulas.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3dd-105">Now, if you want tooadd subsequent VMs tooyour lab, you can also choose a *base* that is either a [custom image](devtest-lab-create-template.md) or a [formula](devtest-lab-manage-formulas.md).</span></span> <span data-ttu-id="3e3dd-106">이 자습서는 Azure 포털 tooadd VM tooa 랩 hello를 사용 하 여에서 DevTest Labs를 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3dd-106">This tutorial walks you through using hello Azure portal tooadd a VM tooa lab in DevTest Labs.</span></span>

<span data-ttu-id="3e3dd-107">또한 이렇게 하면 toomanage 랩에는 VM에 대 한 아티팩트를 hello 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="3e3dd-107">This article also shows you how toomanage hello artifacts for a VM in your lab.</span></span>

## <a name="steps-tooadd-a-vm-tooa-lab-in-azure-devtest-labs"></a><span data-ttu-id="3e3dd-108">단계 tooadd DevTest Labs Azure에서에서 VM tooa 랩</span><span class="sxs-lookup"><span data-stu-id="3e3dd-108">Steps tooadd a VM tooa lab in Azure DevTest Labs</span></span>
1. <span data-ttu-id="3e3dd-109">Toohello 로그인 [Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3dd-109">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="3e3dd-110">선택 **더 서비스**를 선택한 후 **DevTest Labs** hello 목록에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3dd-110">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
1. <span data-ttu-id="3e3dd-111">랩의 hello 목록에서 toocreate hello VM 원하는 hello 랩을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3dd-111">From hello list of labs, select hello lab in which you want toocreate hello VM.</span></span>  
1. <span data-ttu-id="3e3dd-112">Hello 랩에 **개요** 블레이드를 **+ 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3dd-112">On hello lab's **Overview** blade, select **+ Add**.</span></span>  

    ![VM 단추 추가](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. <span data-ttu-id="3e3dd-114">Hello에 **기본 선택** 블레이드에서 hello VM에 대 한 기준 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3dd-114">On hello **Choose a base** blade, select a base for hello VM.</span></span>
1. <span data-ttu-id="3e3dd-115">Hello에 **가상 컴퓨터** 블레이드에서 hello에 hello 새 가상 컴퓨터에 대 한 이름을 입력 **가상 컴퓨터 이름** 입력란.</span><span class="sxs-lookup"><span data-stu-id="3e3dd-115">On hello **Virtual machine** blade, enter a name for hello new virtual machine in hello **Virtual machine name** text box.</span></span>

    ![랩 VM 블레이드](./media/devtest-lab-add-vm/devtestlab-lab-vm-blade.png)

1. <span data-ttu-id="3e3dd-117">입력 한 **사용자 이름** hello 가상 컴퓨터에서 관리자 권한이 부여 되 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3dd-117">Enter a **User Name** that is granted administrator privileges on hello virtual machine.</span></span>  
1. <span data-ttu-id="3e3dd-118">Toouse 원하는에 저장 된 암호 프로그램 [보안 저장소](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store)을 선택 **저장 된 암호를 사용 하 여**, tooyour 암호 (암호)을 해당 하는 키 값을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3dd-118">If you want toouse a password stored in your [secret store](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store), select **Use a saved secret**, and specify a key value that corresponds tooyour secret (password).</span></span> <span data-ttu-id="3e3dd-119">그렇지 않으면 hello 텍스트 필드에 암호를 입력 **값을 입력**합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3dd-119">Otherwise, enter a password in hello text field labeled **Type a value**.</span></span>
1. <span data-ttu-id="3e3dd-120">hello **가상 컴퓨터 디스크 유형** hello 랩에서 hello 가상 컴퓨터에 대 한 허용 되는 저장소 디스크 형식을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3dd-120">hello **Virtual machine disk type** determines which storage disk type is allowed for hello virtual machines in hello lab.</span></span>
1. <span data-ttu-id="3e3dd-121">선택 **가상 컴퓨터 크기** hello 프로세서 코어, RAM 크기 및 hello VM toocreate의 hello 하드 드라이브 크기를 지정 하는 항목을 미리 정의 된 hello 중 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3dd-121">Select **Virtual machine size** and select one of hello predefined items that specify hello processor cores, RAM size, and hello hard drive size of hello VM toocreate.</span></span>
1. <span data-ttu-id="3e3dd-122">선택 **아티팩트** -아티팩트-hello 목록에서 선택 하 고 원하는 tooadd toohello 기본 이미지 hello 아티팩트를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3dd-122">Select **Artifacts** and - from hello list of artifacts - select and configure hello artifacts that you want tooadd toohello base image.</span></span>
    <span data-ttu-id="3e3dd-123">**참고:** 새 tooDevTest 랩 이거나 toohello 참조 아티팩트 구성 [기존 아티팩트 tooa VM 추가](#add-an-existing-artifact-to-a-vm) 섹션 및 다음 완료 되 면 여기로 돌아와 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3dd-123">**Note:** If you're new tooDevTest Labs or configuring artifacts, refer toohello [Add an existing artifact tooa VM](#add-an-existing-artifact-to-a-vm) section, and then return here when finished.</span></span>
1. <span data-ttu-id="3e3dd-124">선택 **고급 설정** tooconfigure hello VM 네트워크 옵션 및 만료 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="3e3dd-124">Select **Advanced settings** tooconfigure hello VM's network options and expiration options.</span></span> 

   <span data-ttu-id="3e3dd-125">tooset 만료 옵션을 선택 hello 달력 아이콘 toospecify hello VM에 날짜를 자동으로 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e3dd-125">tooset an expiration option, choose hello calendar icon toospecify a date on which hello VM will be automatically deleted.</span></span>  <span data-ttu-id="3e3dd-126">기본적으로 VM hello 만료 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3e3dd-126">By default, hello VM will never expire.</span></span> 
1. <span data-ttu-id="3e3dd-127">원하는 tooview 또는 hello Azure 리소스 관리자 템플릿을 복사 하는 경우 참조 toohello [저장 Azure 리소스 관리자 템플릿](#save-azure-resource-manager-template) 섹션을 완료 되 면 여기로 돌아와 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3dd-127">If you want tooview or copy hello Azure Resource Manager template, refer toohello [Save Azure Resource Manager template](#save-azure-resource-manager-template) section, and return here when finished.</span></span>
1. <span data-ttu-id="3e3dd-128">선택 **만들기** tooadd hello VM toohello 랩을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3dd-128">Select **Create** tooadd hello specified VM toohello lab.</span></span>
1. <span data-ttu-id="3e3dd-129">hello 랩 블레이드 hello의 상태를 표시 hello VM 만들기-처음으로 **만들기**,으로 다음 **실행** hello VM을 시작한 후입니다.</span><span class="sxs-lookup"><span data-stu-id="3e3dd-129">hello lab blade displays hello status of hello VM's creation - first as **Creating**, then as **Running** after hello VM has been started.</span></span>

> [!NOTE]
> <span data-ttu-id="3e3dd-130">[Claimable VM 추가](devtest-lab-add-claimable-vm.md) hello 랩의 모든 사용자가 사용 하기 위해 사용할 수 있도록 VM claimable toomake hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3e3dd-130">[Add a claimable VM](devtest-lab-add-claimable-vm.md) shows you how toomake hello VM claimable so that it is available for use by any user in hello lab.</span></span>
>
>

## <a name="add-an-existing-artifact-tooa-vm"></a><span data-ttu-id="3e3dd-131">기존 아티팩트 tooa VM 추가</span><span class="sxs-lookup"><span data-stu-id="3e3dd-131">Add an existing artifact tooa VM</span></span>
<span data-ttu-id="3e3dd-132">VM을 만드는 동안 기존 아티팩트를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e3dd-132">While creating a VM, you can add existing artifacts.</span></span> <span data-ttu-id="3e3dd-133">각 lab hello 공개 DevTest Labs 아티팩트 저장소에서에서 아티팩트와 아티팩트 만든 및 아티팩트 리포지토리를 소유 하는 추가 된 tooyour가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e3dd-133">Each lab includes artifacts from hello Public DevTest Labs Artifact Repository as well as artifacts that you've created and added tooyour own Artifact Repository.</span></span>

* <span data-ttu-id="3e3dd-134">Azure DevTest Labs *아티팩트* 지정할 수 *동작* hello VM 프로 비전 되 면 Windows PowerShell 스크립트 실행, Bash 명령 실행, 소프트웨어 설치 등 때 수행 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3dd-134">Azure DevTest Labs *artifacts* let you specify *actions* that are performed when hello VM is provisioned, such as running Windows PowerShell scripts, running Bash commands, and installing software.</span></span>
* <span data-ttu-id="3e3dd-135">아티팩트 *매개 변수* 특정 시나리오에 대 한 hello 아티팩트를 사용자 지정할 수 있도록</span><span class="sxs-lookup"><span data-stu-id="3e3dd-135">Artifact *parameters* let you customize hello artifact for your particular scenario</span></span>

<span data-ttu-id="3e3dd-136">toocreate 아티팩트를 확인 하려면 어떻게 toodiscover hello 문서, [tooauthor 사용자 고유의 아티팩트에 대 한 포함 된 사용 방법을 DevTest Labs 자세한](devtest-lab-artifact-author.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3dd-136">toodiscover how toocreate artifacts, see hello article, [Learn how tooauthor your own artifacts for use with DevTest Labs](devtest-lab-artifact-author.md).</span></span>

1. <span data-ttu-id="3e3dd-137">Toohello 로그인 [Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3dd-137">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="3e3dd-138">선택 **더 서비스**를 선택한 후 **DevTest Labs** hello 목록에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3dd-138">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
1. <span data-ttu-id="3e3dd-139">랩의 hello 목록에서 toowork 하려는 hello VM이 포함 된 hello 랩을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3dd-139">From hello list of labs, select hello lab containing hello VM with which you want toowork.</span></span>  
1. <span data-ttu-id="3e3dd-140">**내 가상 컴퓨터**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3dd-140">Select **My virtual machines**.</span></span>
1. <span data-ttu-id="3e3dd-141">Select hello 원하는 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="3e3dd-141">Select hello desired VM.</span></span>
1. <span data-ttu-id="3e3dd-142">**아티팩트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3dd-142">Select **Artifacts**.</span></span> 
1. <span data-ttu-id="3e3dd-143">**아티팩트 적용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3dd-143">Select **Apply artifacts**.</span></span>
1. <span data-ttu-id="3e3dd-144">Hello에 **아티팩트 적용** 블레이드, 선택 hello 아티팩트 tooadd toohello VM을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3dd-144">On hello **Apply artifacts** blade, select hello artifact you wish tooadd toohello VM.</span></span>
1. <span data-ttu-id="3e3dd-145">Hello에 **추가 아티팩트** 블레이드에서 필수 hello 매개 변수 값 및 해야 하는 선택적 매개 변수를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3dd-145">On hello **Add artifact** blade, enter hello required parameter values and any optional parameters that you need.</span></span>  
1. <span data-ttu-id="3e3dd-146">선택 **추가** tooadd hello 아티팩트 및 반환 toohello **아티팩트 적용** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="3e3dd-146">Select **Add** tooadd hello artifact and return toohello **Apply artifacts** blade.</span></span>
1. <span data-ttu-id="3e3dd-147">VM에 필요한 만큼 계속해서 아티팩트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3dd-147">Continue adding artifacts as needed for your VM.</span></span>
1. <span data-ttu-id="3e3dd-148">아티팩트를 추가한 후 [는 hello 아티팩트 실행 hello 순서 변경](#change-the-order-in-which-artifacts-are-run)합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3dd-148">Once you've added your artifacts, you can [change hello order in which hello artifacts are run](#change-the-order-in-which-artifacts-are-run).</span></span> <span data-ttu-id="3e3dd-149">또한 뒤로 이동할 수 너무[확인 하거나 수정할 아티팩트](#view-or-modify-an-artifact)합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3dd-149">You can also go back too[view or modify an artifact](#view-or-modify-an-artifact).</span></span>
1. <span data-ttu-id="3e3dd-150">아티팩트 추가를 마친 경우 **적용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3dd-150">When you're done adding artifacts, select **Apply**</span></span>

## <a name="change-hello-order-in-which-artifacts-are-run"></a><span data-ttu-id="3e3dd-151">아티팩트 실행 되는 hello 순서 변경</span><span class="sxs-lookup"><span data-stu-id="3e3dd-151">Change hello order in which artifacts are run</span></span>
<span data-ttu-id="3e3dd-152">기본적으로 hello 아티팩트의 hello 작업이 hello는 추가 순서 대로 toohello VM에서에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e3dd-152">By default, hello actions of hello artifacts are executed in hello order in which they are added toohello VM.</span></span> <span data-ttu-id="3e3dd-153">hello 아래 단계에 설명 방법을 toochange hello는 hello 아티팩트의 실행 순서입니다.</span><span class="sxs-lookup"><span data-stu-id="3e3dd-153">hello following steps illustrate how toochange hello order in which hello artifacts are run.</span></span>

1. <span data-ttu-id="3e3dd-154">Hello의 hello 위쪽 **아티팩트 적용** 블레이드, hello toohello VM에 추가 된 아티팩트 수를 나타내는 선택 hello 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3dd-154">At hello top of hello **Apply artifacts** blade, select hello link indicating hello number of artifacts that have been added toohello VM.</span></span>
   
    ![다양 한 아티팩트 추가 tooVM](./media/devtest-lab-add-vm-with-artifacts/devtestlab-add-artifacts-blade-selected-artifacts.png)
1. <span data-ttu-id="3e3dd-156">Hello에 **아티팩트 선택** 블레이드, 끌어서 놓기 hello 아티팩트 hello 원하는 순서입니다.</span><span class="sxs-lookup"><span data-stu-id="3e3dd-156">On hello **Selected artifacts** blade, drag and drop hello artifacts into hello desired order.</span></span> <span data-ttu-id="3e3dd-157">**참고:** hello 아티팩트를 끄는 데 문제가 있는 경우 hello hello 아티팩트의 왼쪽에서 끌어온 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3dd-157">**Note:** If you have trouble dragging hello artifact, make sure that you are dragging from hello left side of hello artifact.</span></span> 
1. <span data-ttu-id="3e3dd-158">완료되면 **확인** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3dd-158">Select **OK** when done.</span></span>  

## <a name="view-or-modify-an-artifact"></a><span data-ttu-id="3e3dd-159">아티팩트를 확인 또는 수정</span><span class="sxs-lookup"><span data-stu-id="3e3dd-159">View or modify an artifact</span></span>
<span data-ttu-id="3e3dd-160">hello 아래 단계에 설명 방법을 tooview 아티팩트 hello 매개 변수 또는 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3dd-160">hello following steps illustrate how tooview or modify hello parameters of an artifact:</span></span>

1. <span data-ttu-id="3e3dd-161">Hello의 hello 위쪽 **아티팩트 적용** 블레이드, hello toohello VM에 추가 된 아티팩트 수를 나타내는 선택 hello 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3dd-161">At hello top of hello **Apply artifacts** blade, select hello link indicating hello number of artifacts that have been added toohello VM.</span></span>
   
    ![다양 한 아티팩트 추가 tooVM](./media/devtest-lab-add-vm-with-artifacts/devtestlab-add-artifacts-blade-selected-artifacts.png)
1. <span data-ttu-id="3e3dd-163">Hello에 **아티팩트 선택** 블레이드, 선택 hello 아티팩트 tooview 싶거나 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3dd-163">On hello **Selected artifacts** blade, select hello artifact that you want tooview or edit.</span></span>  
1. <span data-ttu-id="3e3dd-164">Hello에 **추가 아티팩트** 블레이드를 변경 필요 하 고 선택 하나 수행 **확인** tooclose hello **추가 아티팩트** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="3e3dd-164">On hello **Add artifact** blade, make any needed changes, and select **OK** tooclose hello **Add artifact** blade.</span></span>
1. <span data-ttu-id="3e3dd-165">선택 **확인** tooclose hello **아티팩트 선택** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="3e3dd-165">Select **OK** tooclose hello **Selected artifacts** blade.</span></span>

## <a name="save-azure-resource-manager-template"></a><span data-ttu-id="3e3dd-166">Azure Resource Manager 템플릿 저장</span><span class="sxs-lookup"><span data-stu-id="3e3dd-166">Save Azure Resource Manager template</span></span>
<span data-ttu-id="3e3dd-167">Azure 리소스 관리자 템플릿을 반복 가능한 배포가 선언적으로 toodefine를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3dd-167">An Azure Resource Manager template provides a declarative way toodefine a repeatable deployment.</span></span> <span data-ttu-id="3e3dd-168">단계를 수행 하는 hello toosave hello 만드는 VM에 대 한 Azure 리소스 관리자 템플릿을 hello 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3dd-168">hello following steps explain how toosave hello Azure Resource Manager template for hello VM being created.</span></span>
<span data-ttu-id="3e3dd-169">저장 한 후 템플릿을 사용 하 여 hello Azure 리소스 관리자 너무[Azure PowerShell을 사용한 새 Vm 배포](../azure-resource-manager/resource-group-overview.md#template-deployment)합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3dd-169">Once saved, you can use hello Azure Resource Manager template too[deploy new VMs with Azure PowerShell](../azure-resource-manager/resource-group-overview.md#template-deployment).</span></span>

1. <span data-ttu-id="3e3dd-170">Hello에 **가상 컴퓨터** 블레이드를 **ARM 템플릿 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3dd-170">On hello **Virtual machine** blade, select **View ARM Template**.</span></span>
2. <span data-ttu-id="3e3dd-171">Hello에 **보기 Azure 리소스 관리자 템플릿** 블레이드, 선택 hello 템플릿 텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="3e3dd-171">On hello **View Azure Resource Manager template** blade, select hello template text.</span></span>
3. <span data-ttu-id="3e3dd-172">Hello 선택한 텍스트 toohello 클립보드에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3dd-172">Copy hello selected text toohello clipboard.</span></span>
4. <span data-ttu-id="3e3dd-173">선택 **확인** tooclose hello **Azure 리소스 관리자 템플릿 보기 블레이드에서**합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3dd-173">Select **OK** tooclose hello **View Azure Resource Manager Template blade**.</span></span>
5. <span data-ttu-id="3e3dd-174">텍스트 편집기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3e3dd-174">Open a text editor.</span></span>
6. <span data-ttu-id="3e3dd-175">Hello 클립보드의 템플릿 텍스트 hello에에서 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="3e3dd-175">Paste in hello template text from hello clipboard.</span></span>
7. <span data-ttu-id="3e3dd-176">나중에 사용할 hello 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3dd-176">Save hello file for later use.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

### <a name="next-steps"></a><span data-ttu-id="3e3dd-177">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3e3dd-177">Next steps</span></span>
* <span data-ttu-id="3e3dd-178">한 번 만든 VM hello, 연결할 수 있습니다 toohello VM을 선택 하 여 **연결** hello VM 블레이드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3dd-178">Once hello VM has been created, you can connect toohello VM by selecting **Connect** on hello VM's blade.</span></span>
* <span data-ttu-id="3e3dd-179">너무 방법에 대해 알아봅니다[DevTest Labs VM에 대 한 사용자 지정 아티팩트를 만들면](devtest-lab-artifact-author.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3dd-179">Learn how too[create custom artifacts for your DevTest Labs VM](devtest-lab-artifact-author.md).</span></span>
* <span data-ttu-id="3e3dd-180">Hello 탐색 [DevTest Labs Azure 리소스 관리자 퀵 스타트 템플릿 갤러리](https://github.com/Azure/azure-devtestlab/tree/master/Samples)합니다.</span><span class="sxs-lookup"><span data-stu-id="3e3dd-180">Explore hello [DevTest Labs Azure Resource Manager QuickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/Samples).</span></span>
