---
title: "Azure DevTest Labs에서 랩에 클레임할 수 있는 VM 추가 | Microsoft Docs"
description: "Azure DevTest Labs에서 랩에 클레임할 수 있는 가상 컴퓨터를 추가하는 방법 알아보기"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: f671e66e-9630-4e30-a131-a6bad9ed9c11
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: tarcher
ms.openlocfilehash: 98950d72e90b0e178bae2fffa7644fd824a25eea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="add-a-claimable-vm-to-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="bcc1f-103">Azure DevTest Labs에서 랩에 클레임할 수 있는 VM 추가</span><span class="sxs-lookup"><span data-stu-id="bcc1f-103">Add a claimable VM to a lab in Azure DevTest Labs</span></span>
<span data-ttu-id="bcc1f-104">클레임할 수 있는 VM은 [표준 VM을 추가](devtest-lab-add-vm.md)하는 것과 유사한 방식으로([사용자 지정 이미지](devtest-lab-create-template.md), [수식](devtest-lab-manage-formulas.md) 또는 [Marketplace 이미지](devtest-lab-configure-marketplace-images.md)를 *기반*으로) 랩에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bcc1f-104">You add a claimable VM to a lab in a similar manner to how you [add a standard VM](devtest-lab-add-vm.md) – from a *base* that is either a [custom image](devtest-lab-create-template.md), [formula](devtest-lab-manage-formulas.md), or [Marketplace image](devtest-lab-configure-marketplace-images.md).</span></span> <span data-ttu-id="bcc1f-105">이 자습서에서는 Azure Portal을 사용하여 클레임할 수 있는 VM을 DevTest Labs의 랩에 추가하는 단계를 안내하고 VM을 클레임하기 위해 따라야 하는 프로세스를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="bcc1f-105">This tutorial walks you through using the Azure portal to add a claimable VM to a lab in DevTest Labs, and shows the process a user follows to claim the VM.</span></span>

> [!NOTE]
> <span data-ttu-id="bcc1f-106">[Azure Resource Manager 템플릿](devtest-lab-create-environment-from-arm.md)을 통해 랩 VM을 배포하는 경우 속성 섹션에서 **allowClaim** 속성을 true로 설정하면 클레임할 수 있는 VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcc1f-106">If you deploy lab VMs through [Azure Resource Manager templates](devtest-lab-create-environment-from-arm.md), you can create claimable VMs by setting the **allowClaim** property to true in the properties section.</span></span>
>
>

## <a name="steps-to-add-a-claimable-vm-to-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="bcc1f-107">Azure DevTest Labs에서 랩에 클레임할 수 있는 VM을 추가하는 단계</span><span class="sxs-lookup"><span data-stu-id="bcc1f-107">Steps to add a claimable VM to a lab in Azure DevTest Labs</span></span>
1. <span data-ttu-id="bcc1f-108">[Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="bcc1f-108">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="bcc1f-109">**추가 서비스**를 선택한 후 목록에서 **DevTest Labs**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bcc1f-109">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
1. <span data-ttu-id="bcc1f-110">랩 목록에서 클레임할 수 있는 VM을 만들려는 랩을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bcc1f-110">From the list of labs, select the lab in which you want to create the claimable VM.</span></span>  
1. <span data-ttu-id="bcc1f-111">랩의 **개요** 블레이드에서 **+ 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bcc1f-111">On the lab's **Overview** blade, select **+ Add**.</span></span>  

    ![VM 단추 추가](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. <span data-ttu-id="bcc1f-113">**기본 선택** 블레이드에서 VM의 기본을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bcc1f-113">On the **Choose a base** blade, select a base for the VM.</span></span>
1. <span data-ttu-id="bcc1f-114">**가상 컴퓨터** 블레이드의 **가상 컴퓨터 이름** 텍스트 상자에 새 가상 컴퓨터의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="bcc1f-114">On the **Virtual machine** blade, enter a name for the new virtual machine in the **Virtual machine name** text box.</span></span>

    ![랩 VM 블레이드](./media/devtest-lab-add-vm/devtestlab-lab-vm-blade.png)

1. <span data-ttu-id="bcc1f-116">가상 컴퓨터에서 관리자 권한이 부여된 **사용자 이름**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="bcc1f-116">Enter a **User Name** that is granted administrator privileges on the virtual machine.</span></span>  
1. <span data-ttu-id="bcc1f-117">[비밀 저장소](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store)에 저장된 암호를 사용하려는 경우 **저장된 비밀 사용**을 선택하고 비밀(암호)에 해당하는 키 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="bcc1f-117">If you want to use a password stored in your [secret store](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store), select **Use a saved secret**, and specify a key value that corresponds to your secret (password).</span></span> <span data-ttu-id="bcc1f-118">그렇지 않으면 **값 입력** 텍스트 필드에 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="bcc1f-118">Otherwise, enter a password in the text field labeled **Type a value**.</span></span>
1. <span data-ttu-id="bcc1f-119">**가상 컴퓨터 디스크 유형**은 랩에서 가상 컴퓨터의 저장소 디스크 유형을 허용하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bcc1f-119">The **Virtual machine disk type** determines which storage disk type is allowed for the virtual machines in the lab.</span></span>
1. <span data-ttu-id="bcc1f-120">**가상 컴퓨터 크기** 를 선택하고 만들려는 프로세서 코어, RAM 크기 및 VM의 하드 드라이브 크기를 지정하는 미리 정의된 항목 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bcc1f-120">Select **Virtual machine size** and select one of the predefined items that specify the processor cores, RAM size, and the hard drive size of the VM to create.</span></span>
1. <span data-ttu-id="bcc1f-121">**아티팩트**를 선택하고 아티팩트 목록에서 기본 이미지에 추가하려는 아티팩트를 선택하고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="bcc1f-121">Select **Artifacts** and from the list of artifacts, select and configure the artifacts that you want to add to the base image.</span></span> <span data-ttu-id="bcc1f-122">DevTest Lab을 처음 접하거나 아티팩트를 구성 중인 경우 [VM에 기존 아티팩트 추가](devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) 섹션을 참조한 다음 완료되면 여기로 돌아옵니다.</span><span class="sxs-lookup"><span data-stu-id="bcc1f-122">If you're new to DevTest Labs or configuring artifacts, refer to the [Add an existing artifact to a VM](devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) section, and then return here when finished.</span></span>
1. <span data-ttu-id="bcc1f-123">**고급 설정**을 선택하여 VM의 네트워크 옵션 및 만료 옵션을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="bcc1f-123">Select **Advanced settings** to configure the VM's network options and expiration options.</span></span> <span data-ttu-id="bcc1f-124">**Claim options(클레임 옵션)**에서 **예**를 선택하여 컴퓨터를 클레임할 수 있도록 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bcc1f-124">Under **Claim options**, choose **Yes** to make the machine claimable.</span></span>

  ![VM을 클레임할 수 있도록 선택합니다.](./media/devtest-lab-add-vm/devtestlab-claim-VM-option.png)

1. <span data-ttu-id="bcc1f-126">Azure Resource Manager 템플릿을 보거나 복사하려면 [Azure Resource Manager 템플릿 저장](devtest-lab-add-vm.md#save-azure-resource-manager-template) 섹션을 참조하여 원하는 작업을 마친 후에 여기로 다시 돌아옵니다.</span><span class="sxs-lookup"><span data-stu-id="bcc1f-126">If you want to view or copy the Azure Resource Manager template, refer to the [Save Azure Resource Manager template](devtest-lab-add-vm.md#save-azure-resource-manager-template) section, and return here when finished.</span></span>
1. <span data-ttu-id="bcc1f-127">**만들기** 를 누르고 지정된 VM을 랩에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bcc1f-127">Select **Create** to add the specified VM to the lab.</span></span>
1. <span data-ttu-id="bcc1f-128">랩 블레이드는 VM의 만들기 상태를 표시합니다. 처음에는 **생성 중**이 표시되고 VM이 시작하면 **실행 중**으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="bcc1f-128">The lab blade displays the status of the VM's creation - first as **Creating**, then as **Running** after the VM has been started.</span></span>


## <a name="using-a-claimable-vm"></a><span data-ttu-id="bcc1f-129">클레임할 수 있는 VM 사용</span><span class="sxs-lookup"><span data-stu-id="bcc1f-129">Using a claimable VM</span></span>

<span data-ttu-id="bcc1f-130">다음 단계 중 하나를 수행하면 “클레임할 수 있는 가상 컴퓨터” 목록에서 원하는 VM을 클레임할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcc1f-130">A user can claim any VM from the list of "Claimable virtual machines" by doing one of these steps:</span></span>

* <span data-ttu-id="bcc1f-131">랩의 개요 블레이드 아래쪽에 있는 “클레임할 수 있는 가상 컴퓨터” 목록에서 VM 중 하나를 마우스 오른쪽 단추로 클릭하고 **Claim machine(컴퓨터 클레임)**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bcc1f-131">From the list of "Claimable virtual machines" at the bottom of the lab's Overview blade, right-click on one of the VMs in the list and choose **Claim machine**.</span></span>

 ![클레임할 수 있는 특정 VM을 요청합니다.](./media/devtest-lab-add-vm/devtestlab-claim-VM.png)


* <span data-ttu-id="bcc1f-133">**개요** 블레이드 맨 위에서 **Claim any(임의 클레임)**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bcc1f-133">At the top of the **Overview** blade, choose **Claim any**.</span></span> <span data-ttu-id="bcc1f-134">클레임할 수 있는 VM 목록에서 임의의 가상 컴퓨터가 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="bcc1f-134">A random virtual machine is assigned from the list of claimable VMs.</span></span>

 ![클레임할 수 있는 임의의 VM을 요청합니다.](./media/devtest-lab-add-vm/devtestlab-claim-any.png)


<span data-ttu-id="bcc1f-136">사용자가 VM을 클레임한 후에는 사용자의 "내 가상 컴퓨터" 목록으로 이동되고 더 이상 다른 사용자가 클레임할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bcc1f-136">After a user claims a VM, it is moved up into their list of "My virtual machines" and is no longer claimable by any other user.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bcc1f-137">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bcc1f-137">Next steps</span></span>
* <span data-ttu-id="bcc1f-138">VM을 만든 후에는 해당 VM의 블레이드에서 **연결** 을 선택하여 VM에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcc1f-138">Once the VM has been created, you can connect to the VM by selecting **Connect** on the VM's blade.</span></span>
* <span data-ttu-id="bcc1f-139">[DevTest Labs Azure Resource Manager 빠른 시작 템플릿 갤러리](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates) 탐색</span><span class="sxs-lookup"><span data-stu-id="bcc1f-139">Explore the [DevTest Labs Azure Resource Manager QuickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates)</span></span>
