---
title: "VM을 만드는 Azure DevTest Labs 수식 관리 | Microsoft 문서"
description: "Azure DevTest Labs 수식을 업데이트하고 제거하는 방법 알아보기"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 841dd95a-657f-4d80-ba26-59a9b5104fe4
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: tarcher
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bfdab5def50158f9b764bbb1e50c2624cc6d5fb3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-azure-devtest-labs-formulas"></a><span data-ttu-id="cf585-103">Azure DevTest Labs 수식 관리</span><span class="sxs-lookup"><span data-stu-id="cf585-103">Manage Azure DevTest Labs formulas</span></span>

[!INCLUDE [devtest-lab-formula-definition](../../includes/devtest-lab-formula-definition.md)]

<span data-ttu-id="cf585-104">이 문서에서는 기본(사용자 지정 이미지, Marketplace 이미지 또는 다른 수식) 또는 기존 VM에서 수식을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cf585-104">This article illustrates how to create a formula from either a base (custom image, Marketplace image, or another formula) or an existing VM.</span></span> <span data-ttu-id="cf585-105">이 문서에서 기존 수식을 관리하는 방법을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="cf585-105">This article also guides you through managing existing formulas.</span></span>

## <a name="create-a-formula"></a><span data-ttu-id="cf585-106">수식 만들기</span><span class="sxs-lookup"><span data-stu-id="cf585-106">Create a formula</span></span>
<span data-ttu-id="cf585-107">DevTest Lab *사용자* 권한이 있으면 수식을 기준으로 사용하여 VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf585-107">Anyone with DevTest Labs *Users* permissions is able to create VMs using a formula as a base.</span></span> <span data-ttu-id="cf585-108">수식을 만드는 방법은 두 가지입니다.</span><span class="sxs-lookup"><span data-stu-id="cf585-108">There are two ways to create formulas:</span></span> 

* <span data-ttu-id="cf585-109">기준에서 - 수식의 모든 특성을 정의하려는 경우에 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cf585-109">From a base - Use when you want to define all the characteristics of the formula.</span></span>
* <span data-ttu-id="cf585-110">기존 랩 VM을 통해 - 기존 VM의 설정을 기반으로 수식을 만들려는 경우에 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cf585-110">From an existing lab VM - Use when you want to create a formula based on the settings of an existing VM.</span></span>

<span data-ttu-id="cf585-111">사용자 및 사용 권한을 추가하는 방법에 대한 자세한 내용은 [Azure DevTest Labs에 소유자 및 사용자 추가](./devtest-lab-add-devtest-user.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cf585-111">For more information about adding users and permissions, see [Add owners and users in Azure DevTest Labs](./devtest-lab-add-devtest-user.md).</span></span>

### <a name="create-a-formula-from-a-base"></a><span data-ttu-id="cf585-112">기준에서 수식 만들기</span><span class="sxs-lookup"><span data-stu-id="cf585-112">Create a formula from a base</span></span>
<span data-ttu-id="cf585-113">다음 단계에서는 사용자 지정 이미지, 마켓플레이스 이미지 또는 다른 수식에서 수식을 만드는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="cf585-113">The following steps guide you through the process of creating a formula from a custom image, Marketplace image, or another formula.</span></span>

1. <span data-ttu-id="cf585-114">[Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="cf585-114">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

2. <span data-ttu-id="cf585-115">**추가 서비스**를 선택한 후 목록에서 **DevTest Labs**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cf585-115">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>

3. <span data-ttu-id="cf585-116">랩 목록에서 원하는 랩을 탭합니다.</span><span class="sxs-lookup"><span data-stu-id="cf585-116">From the list of labs, select the desired lab.</span></span>  

4. <span data-ttu-id="cf585-117">랩의 블레이드에서 **수식(재사용 가능 기준)**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cf585-117">On the lab's blade, select **Formulas (reusable bases)**.</span></span>
   
    ![수식 메뉴](./media/devtest-lab-create-formulas/lab-settings-formulas.png)

5. <span data-ttu-id="cf585-119">**수식** 블레이드에서 **+ 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cf585-119">On the **Formulas** blade, select **+ Add**.</span></span>
   
    ![수식 추가](./media/devtest-lab-create-formulas/add-formula.png)

6. <span data-ttu-id="cf585-121">**기준 선택** 블레이드에서 수식을 만들 때 사용할 기준(사용자 지정 이미지, 마켓플레이스 이미지 또는 수식)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cf585-121">On the **Choose a base** blade, select the base (custom image, Marketplace image, or formula) from which you want to create the formula.</span></span>
   
    ![기본 목록](./media/devtest-lab-create-formulas/base-list.png)

7. <span data-ttu-id="cf585-123">**Create formula** (수식 만들기) 블레이드에서 다음 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="cf585-123">On the **Create formula** blade, specify the following values:</span></span>
   
    * <span data-ttu-id="cf585-124">**수식 이름** - 수식의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="cf585-124">**Formula name** - Enter a name for your formula.</span></span> <span data-ttu-id="cf585-125">이 값은 VM을 만들 때 기본 이미지 목록에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cf585-125">This value is displayed in the list of base images when you create a VM.</span></span> <span data-ttu-id="cf585-126">이름 입력 시에 유효성이 검사되고, 유효하지 않으면, 유효한 이름에 필요한 사항을 알려주는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cf585-126">The name is validated as you type it, and if not valid, a message indicates the requirements for a valid name.</span></span>
    * <span data-ttu-id="cf585-127">**설명** - 수식에 대한 의미 있는 설명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="cf585-127">**Description** - Enter a meaningful description for your formula.</span></span> <span data-ttu-id="cf585-128">이 값은 VM을 만들 때 수식의 상황에 맞는 메뉴에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf585-128">This value is available from the formula's context menu when you create a VM.</span></span>
    * <span data-ttu-id="cf585-129">**사용자 이름** - 관리자 권한이 부여된 사용자 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="cf585-129">**User name** - Enter a user name that is granted administrator privileges.</span></span>
    * <span data-ttu-id="cf585-130">**암호** - 지정된 사용자에 대해 사용하려는 암호와 연결된 값을 입력하거나 드롭다운 목록에서 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cf585-130">**Password** - Enter - or select from the dropdown - a value that is associated with the secret (password) that you want to use for the specified user.</span></span> <span data-ttu-id="cf585-131">비밀에 대한 자세한 내용은 [Azure DevTest Labs: 개인 비밀 저장소](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cf585-131">For more information about the secrets, see [Azure DevTest Labs: Personal secret store](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store/).</span></span>
    * <span data-ttu-id="cf585-132">**가상 컴퓨터 디스크 유형** - HDD(하드 디스크 드라이브) 또는 SSD(반도체 드라이브)를 지정하여 이 기본 이미지를 사용하여 프로비전된 가상 컴퓨터에 허용된 저장소 디스크 유형을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="cf585-132">**Virtual machine disk type** - Specify either HDD (hard-disk drive) or SSD (solid-state drive) to indicate which storage disk type is allowed for the virtual machines provisioned using this base image.</span></span>
    * <span data-ttu-id="cf585-133">**가상 컴퓨터 크기** - 만들려는 VM의 프로세서 코어, RAM 크기 및 하드 드라이브 크기를 지정하는 미리 정의된 항목 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cf585-133">** Virtual machine size** - Select one of the predefined items that specify the processor cores, RAM size, and the hard drive size of the VM to create.</span></span> 
    * <span data-ttu-id="cf585-134">**아티팩트** - **아티팩트 추가** 블레이드를 선택하여 열고 여기에서 기본 이미지에 추가하려는 아티팩트를 선택하고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="cf585-134">**Artifacts** - Select to open the **Add artifacts** blade, in which you select and configure the artifacts that you want to add to the base image.</span></span> <span data-ttu-id="cf585-135">아티팩트에 대한 자세한 내용은 [Azure DevTest Labs에서 VM 아티팩트 관리](./devtest-lab-add-vm-with-artifacts.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cf585-135">For more information about artifacts, see [Manage VM artifacts in Azure DevTest Labs](./devtest-lab-add-vm-with-artifacts.md).</span></span>
    * <span data-ttu-id="cf585-136">**고급 설정** - **고급** 블레이드를 선택하여 열고 다음 설정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="cf585-136">**Advanced settings** - Select to open the **Advanced** blade where you configure the following settings:</span></span>
        * <span data-ttu-id="cf585-137">**가상 네트워크** - 원하는 가상 네트워크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cf585-137">**Virtual network** - Specify the desired virtual network.</span></span>
        * <span data-ttu-id="cf585-138">**서브넷** - 원하는 서브넷을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="cf585-138">**Subnet** - Specify the desired subnet.</span></span>    
        * <span data-ttu-id="cf585-139">**IP 주소 구성** - 공용, 개인 또는 공유 IP 주소를 원하는 경우 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="cf585-139">**IP address configuration** - Specify if you want the Public, Private, or Shared IP addresses.</span></span> <span data-ttu-id="cf585-140">공유 IP 주소에 대한 자세한 내용은 [Azure DevTest Labs에서 공유 IP 주소 이해](./devtest-lab-shared-ip.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cf585-140">For more information about shared IP addresses, see [Understand shared IP addresses in Azure DevTest Labs](./devtest-lab-shared-ip.md).</span></span>
        * <span data-ttu-id="cf585-141">**Make this machine claimable**(이 컴퓨터를 클레임 가능하도록 지정) - 컴퓨터를 "클레임 가능"하도록 지정하는 것은 생성 시 소유권을 할당하지 않는다는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="cf585-141">**Make this machine claimable** - Making a machine "claimable" means that it will not be assigned ownership at the time of creation.</span></span> <span data-ttu-id="cf585-142">대신 랩 사용자가 랩의 블레이드에서 컴퓨터에 대한 소유권("클레임")을 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf585-142">Instead lab users will be able to take ownership ("claim") the machine in the lab's blade.</span></span>     
    * <span data-ttu-id="cf585-143">**이미지** - 이 필드는 이전 블레이드에서 선택한 기본 이미지의 이름을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="cf585-143">**Image** - This field displays name of the base image you selected on the previous blade.</span></span> 
     
       ![Create formula](./media/devtest-lab-create-formulas/create-formula.png)

8. <span data-ttu-id="cf585-145">**만들기** 를 탭하여 수식을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cf585-145">Select **Create** to create the formula.</span></span>

9. <span data-ttu-id="cf585-146">수식이 만들어지면, **수식** 블레이드 목록에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cf585-146">When the formula has been created, it displays in the list on the **Formulas** blade.</span></span>

### <a name="create-a-formula-from-a-vm"></a><span data-ttu-id="cf585-147">VM에서 수식 만들기</span><span class="sxs-lookup"><span data-stu-id="cf585-147">Create a formula from a VM</span></span>
<span data-ttu-id="cf585-148">다음 단계는 기존 VM을 기반으로 수식을 만드는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="cf585-148">The following steps guide you through the process of creating a formula based on an existing VM.</span></span> 

> [!NOTE]
> <span data-ttu-id="cf585-149">VM에서 수식을 만들려면 2016년 3월 30일 이후에 VM을 만들었어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf585-149">To create a formula from a VM, the VM must have been created after March 30, 2016.</span></span> 
> 
> 

1. <span data-ttu-id="cf585-150">[Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="cf585-150">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="cf585-151">**추가 서비스**를 선택한 후 목록에서 **DevTest Labs**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cf585-151">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="cf585-152">랩 목록에서 원하는 랩을 탭합니다.</span><span class="sxs-lookup"><span data-stu-id="cf585-152">From the list of labs, select the desired lab.</span></span>  
4. <span data-ttu-id="cf585-153">랩의 **개요** 블레이드에서 수식을 만들 VM을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cf585-153">On the lab's **Overview** blade, select the VM from which you wish to create the formula.</span></span>
   
    ![랩 VM](./media/devtest-lab-create-formulas/my-vms.png)
5. <span data-ttu-id="cf585-155">VM 블레이드에서 **수식 만들기(재사용 가능 기준)**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cf585-155">On the VM's blade, select **Create formula (reusable base)**.</span></span>
   
    ![Create formula](./media/devtest-lab-create-formulas/create-formula-menu.png)
6. <span data-ttu-id="cf585-157">**수식 만들기** 블레이드에서 새 수식의 **이름** 및 **설명** 을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="cf585-157">On the **Create formula** blade, enter a **Name** and **Description** for your new formula.</span></span>
   
    ![수식 만들기 블레이드](./media/devtest-lab-create-formulas/create-formula-blade.png)
7. <span data-ttu-id="cf585-159">**확인** 을 선택하여 수식을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cf585-159">Select **OK** to create the formula.</span></span>

## <a name="modify-a-formula"></a><span data-ttu-id="cf585-160">수식 수정</span><span class="sxs-lookup"><span data-stu-id="cf585-160">Modify a formula</span></span>
<span data-ttu-id="cf585-161">수식을 수정하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="cf585-161">To modify a formula, follow these steps:</span></span>

1. <span data-ttu-id="cf585-162">[Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="cf585-162">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="cf585-163">**추가 서비스**를 선택한 후 목록에서 **DevTest Labs**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cf585-163">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="cf585-164">랩 목록에서 원하는 랩을 탭합니다.</span><span class="sxs-lookup"><span data-stu-id="cf585-164">From the list of labs, select the desired lab.</span></span>  
4. <span data-ttu-id="cf585-165">랩의 블레이드에서 **수식(재사용 가능 기준)**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cf585-165">On the lab's blade, select **Formulas (reusable bases)**.</span></span>
   
    ![수식 메뉴](./media/devtest-lab-manage-formulas/lab-settings-formulas.png)
5. <span data-ttu-id="cf585-167">**Lab formulas** (랩 수식) 블레이드에서 수정할 수식을 탭합니다.</span><span class="sxs-lookup"><span data-stu-id="cf585-167">On the **Lab formulas** blade, select the formula you wish to modify.</span></span>
6. <span data-ttu-id="cf585-168">**수식 업데이트** 블레이드에서 원하는 내용을 편집하고 **업데이트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cf585-168">On the **Update formula** blade, make the desired edits, and select **Update**.</span></span>

## <a name="delete-a-formula"></a><span data-ttu-id="cf585-169">수식 삭제</span><span class="sxs-lookup"><span data-stu-id="cf585-169">Delete a formula</span></span>
<span data-ttu-id="cf585-170">수식을 삭제하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="cf585-170">To delete a formula, follow these steps:</span></span>

1. <span data-ttu-id="cf585-171">[Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="cf585-171">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="cf585-172">**추가 서비스**를 선택한 후 목록에서 **DevTest Labs**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cf585-172">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="cf585-173">랩 목록에서 원하는 랩을 탭합니다.</span><span class="sxs-lookup"><span data-stu-id="cf585-173">From the list of labs, select the desired lab.</span></span>  
4. <span data-ttu-id="cf585-174">랩의 **설정** 블레이드에서 **수식**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cf585-174">On the lab **Settings** blade, select **Formulas**.</span></span>
   
    ![수식 메뉴](./media/devtest-lab-manage-formulas/lab-settings-formulas.png)
5. <span data-ttu-id="cf585-176">**Lab formulas** (랩 수식) 블레이드에서 삭제할 수식 오른쪽의 줄임표를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cf585-176">On the **Lab formulas** blade, select the ellipsis to the right of the formula you wish to delete.</span></span>
   
    ![수식 메뉴](./media/devtest-lab-manage-formulas/lab-formulas-blade.png)
6. <span data-ttu-id="cf585-178">수식의 상황에 맞는 메뉴에서 **삭제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cf585-178">On the formula's context menu, select **Delete**.</span></span>
   
    ![수식 상황에 맞는 메뉴](./media/devtest-lab-manage-formulas/formula-delete-context-menu.png)
7. <span data-ttu-id="cf585-180">삭제 확인 대화 상자에서 **예** 를 탭합니다.</span><span class="sxs-lookup"><span data-stu-id="cf585-180">Select **Yes** to the deletion confirmation dialog.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="cf585-181">관련 블로그 게시물</span><span class="sxs-lookup"><span data-stu-id="cf585-181">Related blog posts</span></span>
* [<span data-ttu-id="cf585-182">사용자 지정 이미지 또는 수식?</span><span class="sxs-lookup"><span data-stu-id="cf585-182">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)

## <a name="next-steps"></a><span data-ttu-id="cf585-183">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cf585-183">Next steps</span></span>
<span data-ttu-id="cf585-184">VM을 만들 때 사용할 수식을 만들었으면 다음 단계는 [VM을 랩에 추가](devtest-lab-add-vm-with-artifacts.md)하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="cf585-184">Once you have created a formula for use when creating a VM, the next step is to [add a VM to your lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

