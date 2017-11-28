---
title: "aaaCreate 첫 번째 VM에 Azure DevTest Labs 랩에서 | Microsoft Docs"
description: "자세한 내용은 방법 toocreate Azure DevTest Labs에 랩의 첫 번째 가상 컴퓨터"
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
ms.openlocfilehash: 4c3257efca9be6fdd190eaac1db731464e07fcfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-vm-in-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="095c6-103">Azure DevTest Labs에서 첫 번째 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="095c6-103">Create your first VM in a lab in Azure DevTest Labs</span></span>

<span data-ttu-id="095c6-104">처음에 DevTest Labs를 액세스 하 고 첫 번째 VM toocreate 원하는 있습니다 때 가능성이 이렇게 하려면 미리 로드를 사용 하 여 [기본 마켓플레이스 이미지](devtest-lab-configure-marketplace-images.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="095c6-104">When you initially access DevTest Labs and want toocreate your first VM, you will likely do so using a pre-loaded [base marketplace image](devtest-lab-configure-marketplace-images.md).</span></span> <span data-ttu-id="095c6-105">나중에 수 있습니다 수 toochoose에서는 [수식 및 사용자 지정 이미지](devtest-lab-add-vm.md) 더 많은 Vm을 만들 때.</span><span class="sxs-lookup"><span data-stu-id="095c6-105">Later on, you'll also be able toochoose from a [custom image and a formula](devtest-lab-add-vm.md) when creating more VMs.</span></span> 

<span data-ttu-id="095c6-106">이 자습서에서는 Azure 포털 tooadd hello를 사용 하 여 첫 번째 VM tooa 랩에서 DevTest Labs 합니다.</span><span class="sxs-lookup"><span data-stu-id="095c6-106">This tutorial walks you through using hello Azure portal tooadd your first VM tooa lab in DevTest Labs.</span></span>

## <a name="steps-tooadd-your-first-vm-tooa-lab-in-azure-devtest-labs"></a><span data-ttu-id="095c6-107">Azure DevTest Labs로 첫 번째 VM tooa 랩을 tooadd 단계</span><span class="sxs-lookup"><span data-stu-id="095c6-107">Steps tooadd your first VM tooa lab in Azure DevTest Labs</span></span>
1. <span data-ttu-id="095c6-108">Toohello 로그인 [Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)합니다.</span><span class="sxs-lookup"><span data-stu-id="095c6-108">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="095c6-109">선택 **더 서비스**를 선택한 후 **DevTest Labs** hello 목록에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="095c6-109">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
1. <span data-ttu-id="095c6-110">랩의 hello 목록에서 toocreate hello VM 원하는 hello 랩을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="095c6-110">From hello list of labs, select hello lab in which you want toocreate hello VM.</span></span>  
1. <span data-ttu-id="095c6-111">Hello 랩에 **개요** 블레이드를 **+ 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="095c6-111">On hello lab's **Overview** blade, select **+ Add**.</span></span>  

    ![VM 단추 추가](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. <span data-ttu-id="095c6-113">Hello에 **기본 선택** 블레이드, 선택는 마켓플레이스 이미지 hello VM에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="095c6-113">On hello **Choose a base** blade, select a marketplace image for hello VM.</span></span>
1. <span data-ttu-id="095c6-114">Hello에 **가상 컴퓨터** 블레이드에서 hello에 hello 새 가상 컴퓨터에 대 한 이름을 입력 **가상 컴퓨터 이름** 입력란.</span><span class="sxs-lookup"><span data-stu-id="095c6-114">On hello **Virtual machine** blade, enter a name for hello new virtual machine in hello **Virtual machine name** text box.</span></span>

    ![랩 VM 블레이드](./media/devtest-lab-add-vm/devtestlab-lab-add-first-vm.png)

1. <span data-ttu-id="095c6-116">입력 한 **사용자 이름** hello 가상 컴퓨터에서 관리자 권한이 부여 되 합니다.</span><span class="sxs-lookup"><span data-stu-id="095c6-116">Enter a **User Name** that is granted administrator privileges on hello virtual machine.</span></span>  
1. <span data-ttu-id="095c6-117">레이블이 지정 된 hello 텍스트 필드에 암호를 입력 **값을 입력**합니다.</span><span class="sxs-lookup"><span data-stu-id="095c6-117">Enter a password in hello text field labeled **Type a value**.</span></span>
1. <span data-ttu-id="095c6-118">hello **가상 컴퓨터 디스크 유형** hello 랩에서 hello 가상 컴퓨터에 대 한 허용 되는 저장소 디스크 형식을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="095c6-118">hello **Virtual machine disk type** determines which storage disk type is allowed for hello virtual machines in hello lab.</span></span>
1. <span data-ttu-id="095c6-119">선택 **가상 컴퓨터 크기** hello 프로세서 코어, RAM 크기 및 hello VM toocreate의 hello 하드 드라이브 크기를 지정 하는 항목을 미리 정의 된 hello 중 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="095c6-119">Select **Virtual machine size** and select one of hello predefined items that specify hello processor cores, RAM size, and hello hard drive size of hello VM toocreate.</span></span>
1. <span data-ttu-id="095c6-120">선택 **아티팩트** -아티팩트-hello 목록에서 선택 하 고 원하는 tooadd toohello 기본 이미지 hello 아티팩트를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="095c6-120">Select **Artifacts** and - from hello list of artifacts - select and configure hello artifacts that you want tooadd toohello base image.</span></span>
    <span data-ttu-id="095c6-121">**참고:** 새 tooDevTest 랩 이거나 toohello 참조 아티팩트 구성 [기존 아티팩트 tooa VM 추가](./devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) 섹션 및 다음 완료 되 면 여기로 돌아와 합니다.</span><span class="sxs-lookup"><span data-stu-id="095c6-121">**Note:** If you're new tooDevTest Labs or configuring artifacts, refer toohello [Add an existing artifact tooa VM](./devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) section, and then return here when finished.</span></span>
1. <span data-ttu-id="095c6-122">선택 **만들기** tooadd hello VM toohello 랩을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="095c6-122">Select **Create** tooadd hello specified VM toohello lab.</span></span>

   <span data-ttu-id="095c6-123">hello 랩 블레이드 hello의 상태를 표시 hello VM 만들기-처음으로 **만들기**,으로 다음 **실행** hello VM을 시작한 후입니다.</span><span class="sxs-lookup"><span data-stu-id="095c6-123">hello lab blade displays hello status of hello VM's creation - first as **Creating**, then as **Running** after hello VM has been started.</span></span>

## <a name="next-steps"></a><span data-ttu-id="095c6-124">다음 단계</span><span class="sxs-lookup"><span data-stu-id="095c6-124">Next steps</span></span>
* <span data-ttu-id="095c6-125">한 번 만든 VM hello, 연결할 수 있습니다 toohello VM을 선택 하 여 **연결** hello VM 블레이드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="095c6-125">Once hello VM has been created, you can connect toohello VM by selecting **Connect** on hello VM's blade.</span></span>
* <span data-ttu-id="095c6-126">체크 아웃 [추가 VM tooa 랩](devtest-lab-add-vm.md) 랩에서 다음 Vm을 추가 하는 방법에 대 한 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="095c6-126">Check out [Add a VM tooa lab](devtest-lab-add-vm.md) for more complete info about adding subsequent VMs in your lab.</span></span>
* <span data-ttu-id="095c6-127">Hello 탐색 [DevTest Labs Azure 리소스 관리자 퀵 스타트 템플릿 갤러리](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates)합니다.</span><span class="sxs-lookup"><span data-stu-id="095c6-127">Explore hello [DevTest Labs Azure Resource Manager QuickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates).</span></span>
