---
title: "Azure DevTest Labs에서 첫 번째 VM 만들기 | Microsoft Docs"
description: "Azure DevTest Labs에서 랩에 첫 번째 가상 컴퓨터를 만드는 방법 알아보기"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: fbc5a438-6e02-4952-b654-b8fa7322ae5f
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/24/2017
ms.author: tarcher
ms.openlocfilehash: aa6b60b799e1e98815cf288d5612f98cd77cc00e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-your-first-vm-in-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="65aa5-103">Azure DevTest Labs에서 첫 번째 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="65aa5-103">Create your first VM in a lab in Azure DevTest Labs</span></span>

<span data-ttu-id="65aa5-104">DevTest Labs에 처음에 액세스하고 첫 번째 VM을 만드는 경우 미리 로드된 [기본 Marketplace 이미지](devtest-lab-configure-marketplace-images.md)를 사용하여 수행할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="65aa5-104">When you initially access DevTest Labs and want to create your first VM, you will likely do so using a pre-loaded [base marketplace image](devtest-lab-configure-marketplace-images.md).</span></span> <span data-ttu-id="65aa5-105">나중에 VM을 더 만들 때 [사용자 지정 이미지와 수식](devtest-lab-add-vm.md) 중에서 선택할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65aa5-105">Later on, you'll also be able to choose from a [custom image and a formula](devtest-lab-add-vm.md) when creating more VMs.</span></span> 

<span data-ttu-id="65aa5-106">이 자습서에서는 DevTest Labs에서 랩에 첫 번째 VM을 추가하기 위해 Azure Portal을 사용하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="65aa5-106">This tutorial walks you through using the Azure portal to add your first VM to a lab in DevTest Labs.</span></span>

## <a name="steps-to-add-your-first-vm-to-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="65aa5-107">Azure DevTest Labs에서 랩에 첫 번째 VM을 추가하는 단계</span><span class="sxs-lookup"><span data-stu-id="65aa5-107">Steps to add your first VM to a lab in Azure DevTest Labs</span></span>
1. <span data-ttu-id="65aa5-108">[Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="65aa5-108">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="65aa5-109">**추가 서비스**를 선택한 후 목록에서 **DevTest Labs**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="65aa5-109">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
1. <span data-ttu-id="65aa5-110">랩 목록에서 VM을 만들려는 랩을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="65aa5-110">From the list of labs, select the lab in which you want to create the VM.</span></span>  
1. <span data-ttu-id="65aa5-111">랩의 **개요** 블레이드에서 **+ 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="65aa5-111">On the lab's **Overview** blade, select **+ Add**.</span></span>  

    ![VM 단추 추가](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. <span data-ttu-id="65aa5-113">**기본 선택** 블레이드에서 VM의 Marketplace 이미지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="65aa5-113">On the **Choose a base** blade, select a marketplace image for the VM.</span></span>
1. <span data-ttu-id="65aa5-114">**가상 컴퓨터** 블레이드의 **가상 컴퓨터 이름** 텍스트 상자에 새 가상 컴퓨터의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="65aa5-114">On the **Virtual machine** blade, enter a name for the new virtual machine in the **Virtual machine name** text box.</span></span>

    ![랩 VM 블레이드](./media/devtest-lab-add-vm/devtestlab-lab-add-first-vm.png)

1. <span data-ttu-id="65aa5-116">가상 컴퓨터에서 관리자 권한이 부여된 **사용자 이름**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="65aa5-116">Enter a **User Name** that is granted administrator privileges on the virtual machine.</span></span>  
1. <span data-ttu-id="65aa5-117">**값 입력** 텍스트 필드에 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="65aa5-117">Enter a password in the text field labeled **Type a value**.</span></span>
1. <span data-ttu-id="65aa5-118">**가상 컴퓨터 디스크 유형**은 랩에서 가상 컴퓨터의 저장소 디스크 유형을 허용하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="65aa5-118">The **Virtual machine disk type** determines which storage disk type is allowed for the virtual machines in the lab.</span></span>
1. <span data-ttu-id="65aa5-119">**가상 컴퓨터 크기** 를 선택하고 만들려는 프로세서 코어, RAM 크기 및 VM의 하드 드라이브 크기를 지정하는 미리 정의된 항목 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="65aa5-119">Select **Virtual machine size** and select one of the predefined items that specify the processor cores, RAM size, and the hard drive size of the VM to create.</span></span>
1. <span data-ttu-id="65aa5-120">**아티팩트** 를 선택하고 아티팩트 목록에서 기본 이미지에 추가하려는 아티팩트를 선택하고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="65aa5-120">Select **Artifacts** and - from the list of artifacts - select and configure the artifacts that you want to add to the base image.</span></span>
    <span data-ttu-id="65aa5-121">**참고:** DevTest Lab을 처음 접하거나 아티팩트를 구성 중인 경우 [VM에 기존 아티팩트 추가](./devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) 섹션을 참조한 다음 완료되면 여기로 돌아옵니다.</span><span class="sxs-lookup"><span data-stu-id="65aa5-121">**Note:** If you're new to DevTest Labs or configuring artifacts, refer to the [Add an existing artifact to a VM](./devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) section, and then return here when finished.</span></span>
1. <span data-ttu-id="65aa5-122">**만들기** 를 누르고 지정된 VM을 랩에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="65aa5-122">Select **Create** to add the specified VM to the lab.</span></span>

   <span data-ttu-id="65aa5-123">랩 블레이드는 VM의 만들기 상태를 표시합니다. 처음에는 **생성 중**이 표시되고 VM이 시작하면 **실행 중**으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="65aa5-123">The lab blade displays the status of the VM's creation - first as **Creating**, then as **Running** after the VM has been started.</span></span>

## <a name="next-steps"></a><span data-ttu-id="65aa5-124">다음 단계</span><span class="sxs-lookup"><span data-stu-id="65aa5-124">Next steps</span></span>
* <span data-ttu-id="65aa5-125">VM을 만든 후에는 해당 VM의 블레이드에서 **연결** 을 선택하여 VM에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65aa5-125">Once the VM has been created, you can connect to the VM by selecting **Connect** on the VM's blade.</span></span>
* <span data-ttu-id="65aa5-126">이후의 VM을 랩에 추가하는 방법에 대한 자세한 정보는 [랩에 VM 추가](devtest-lab-add-vm.md)를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="65aa5-126">Check out [Add a VM to a lab](devtest-lab-add-vm.md) for more complete info about adding subsequent VMs in your lab.</span></span>
* <span data-ttu-id="65aa5-127">[DevTest Labs Azure Resource Manager 빠른 시작 템플릿 갤러리](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates)를 탐색합니다.</span><span class="sxs-lookup"><span data-stu-id="65aa5-127">Explore the [DevTest Labs Azure Resource Manager QuickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates).</span></span>
