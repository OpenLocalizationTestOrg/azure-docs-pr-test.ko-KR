---
title: "Azure DevTest Labs에서 랩 만들기 | Microsoft Docs"
description: "가상 컴퓨터에 대한 Azure DevTest Labs에서 랩 만들기"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 8b6d3e70-6528-42a4-a2ef-449575d0f928
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/30/2017
ms.author: tarcher
ms.openlocfilehash: 265a968f902f53c7561c8c7e937f8eacfdb37167
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="9f8d8-103">Azure DevTest Labs에서 랩 만들기</span><span class="sxs-lookup"><span data-stu-id="9f8d8-103">Create a lab in Azure DevTest Labs</span></span>
<span data-ttu-id="9f8d8-104">Azure DevTest Labs에서 랩은 VM(Virtual Machines)과 같은 리소스 그룹을 포함하는 인프라로서, 이를 통해 한도 및 할당량을 지정하여 해당 리소스를 더 잘 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f8d8-104">A lab in Azure DevTest Labs is the infrastructure that encompasses a group of resources, such as Virtual Machines (VMs), that lets you better manage those resources by specifying limits and quotas.</span></span> <span data-ttu-id="9f8d8-105">이 문서는 Azure Portal을 사용하여 랩을 만드는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="9f8d8-105">This article walks you through the process of creating a lab using the Azure portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9f8d8-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="9f8d8-106">Prerequisites</span></span>
<span data-ttu-id="9f8d8-107">랩을 만들려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9f8d8-107">To create a lab, you need:</span></span>

* <span data-ttu-id="9f8d8-108">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="9f8d8-108">An Azure subscription.</span></span> <span data-ttu-id="9f8d8-109">Azure 구입 옵션에 대해 알아보려면 [Azure 구입 방법](https://azure.microsoft.com/pricing/purchase-options/) 또는 [1개월 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9f8d8-109">To learn about Azure purchase options, see [How to buy Azure](https://azure.microsoft.com/pricing/purchase-options/) or [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="9f8d8-110">랩을 만들려면 구독 소유자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f8d8-110">You must be the owner of the subscription to create the lab.</span></span>

## <a name="steps-to-create-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="9f8d8-111">Azure DevTest Labs에서 랩을 만드는 단계</span><span class="sxs-lookup"><span data-stu-id="9f8d8-111">Steps to create a lab in Azure DevTest Labs</span></span>
<span data-ttu-id="9f8d8-112">다음 단계는 Azure Portal을 사용하여 Azure DevTest Labs에서 랩을 만드는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="9f8d8-112">The following steps illustrate how to use the Azure portal to create a lab in Azure DevTest Labs.</span></span> 

1. <span data-ttu-id="9f8d8-113">[Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="9f8d8-113">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="9f8d8-114">왼쪽에서 주 메뉴에서 **추가 서비스**(목록 맨 위)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9f8d8-114">From the main menu on the left side, select **More Services** (at the bottom of the list).</span></span>

    ![추가 서비스 메뉴 옵션](./media/devtest-lab-create-lab/more-services-menu-option.png)

1. <span data-ttu-id="9f8d8-116">사용 가능한 서비스 목록에서 **DevTest Labs**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9f8d8-116">From the list of available services, **DevTest Labs**.</span></span>
1. <span data-ttu-id="9f8d8-117">**DevTest Labs** 블레이드에서 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9f8d8-117">On the **DevTest Labs** blade, select **Add**.</span></span>
   
    ![랩 추가](./media/devtest-lab-create-lab/add-lab-button.png)

1. <span data-ttu-id="9f8d8-119">**DevTest Lab 만들기** 블레이드에서</span><span class="sxs-lookup"><span data-stu-id="9f8d8-119">On the **Create a DevTest Lab** blade:</span></span>
   
    1. <span data-ttu-id="9f8d8-120">새 랩에 대한 **랩 이름** 을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9f8d8-120">Enter a **Lab Name** for the new lab.</span></span>
    2. <span data-ttu-id="9f8d8-121">**구독** 을 선택하여 랩과 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="9f8d8-121">Select the **Subscription** to associate with the lab.</span></span>
    3. <span data-ttu-id="9f8d8-122">랩을 저장할 **위치** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9f8d8-122">Select a **Location** in which to store the lab.</span></span>
    4. <span data-ttu-id="9f8d8-123">**자동 종료** 를 선택하여 사용하려는지를 지정하고 랩의 VM을 모두 자동 종료하는 매개 변수를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f8d8-123">Select **Auto-shutdown** to specify if you want to enable - and define the parameters for - the automatic shutting down of all the lab's VMs.</span></span> <span data-ttu-id="9f8d8-124">자동 종료 기능은 주로 VM을 자동으로 종료하려는 경우를 지정할 수 있는 비용 절감 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="9f8d8-124">The auto-shutdown feature is mainly a cost-saving feature whereby you can specify when you want the VM to automatically be shut down.</span></span> <span data-ttu-id="9f8d8-125">[Azure DevTest Labs에서 랩에 대한 모든 정책 관리](./devtest-lab-set-lab-policy.md#set-auto-shutdown) 문서에 간략히 나와 있는 단계에 따라 랩을 만든 후 자동 종료 설정을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f8d8-125">You can change auto-shutdown settings after creating the lab by following the steps outlined in the article, [Manage all policies for a lab in Azure DevTest Labs](./devtest-lab-set-lab-policy.md#set-auto-shutdown).</span></span>
    5. <span data-ttu-id="9f8d8-126">랩 바로 가기를 포털 대시보드에 표시하려면 **대시보드에 고정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9f8d8-126">Select **Pin to Dashboard** if you want a shortcut of the lab to appear on the portal dashboard.</span></span>
    6. <span data-ttu-id="9f8d8-127">구성 자동화를 위한 Azure Resource Manager 템플릿을 가져오려면 **자동화 옵션**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9f8d8-127">Select **Automation options** to get Azure Resource Manager templates for configuration automation.</span></span> 
    7. <span data-ttu-id="9f8d8-128">**만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9f8d8-128">Select **Create**.</span></span> <span data-ttu-id="9f8d8-129">**만들기**를 선택하면 **DevTest Labs** 블레이드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f8d8-129">After selecting **Create**, the **DevTest Labs** blade displays.</span></span> <span data-ttu-id="9f8d8-130">**알림** 영역을 확인하여 랩 만들기 프로세스 상태를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f8d8-130">You can monitor the status of the lab creation process by watching the **Notifications** area.</span></span> <span data-ttu-id="9f8d8-131">완료되면 페이지를 새로 고쳐 랩 목록에서 새로 만들어진 랩을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f8d8-131">Once completed, refresh the page to see the newly created lab in the list of labs.</span></span>  
    
    ![랩 블레이드 만들기](./media/devtest-lab-create-lab/create-devtestlab-blade.png)

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="9f8d8-133">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9f8d8-133">Next steps</span></span>
<span data-ttu-id="9f8d8-134">랩을 만들었으면 다음 단계를 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f8d8-134">Once you've created your lab, here are some next steps to consider:</span></span>

* <span data-ttu-id="9f8d8-135">[랩에 안전하게 액세스](devtest-lab-add-devtest-user.md).</span><span class="sxs-lookup"><span data-stu-id="9f8d8-135">[Secure access to a lab](devtest-lab-add-devtest-user.md).</span></span>
* <span data-ttu-id="9f8d8-136">[랩 정책 설정](devtest-lab-set-lab-policy.md).</span><span class="sxs-lookup"><span data-stu-id="9f8d8-136">[Set lab policies](devtest-lab-set-lab-policy.md).</span></span>
* <span data-ttu-id="9f8d8-137">[랩 템플릿 만들기](devtest-lab-create-template.md).</span><span class="sxs-lookup"><span data-stu-id="9f8d8-137">[Create a lab template](devtest-lab-create-template.md).</span></span>
* <span data-ttu-id="9f8d8-138">[VM에 대한 사용자 지정 아티팩트  만들기](devtest-lab-artifact-author.md).</span><span class="sxs-lookup"><span data-stu-id="9f8d8-138">[Create custom artifacts for your VMs](devtest-lab-artifact-author.md).</span></span>
* <span data-ttu-id="9f8d8-139">[아티팩트가 지정된 VM을 랩에 추가](https://azure.microsoft.com/resources/videos/how-to-create-vms-with-artifacts-in-a-devtest-lab/).</span><span class="sxs-lookup"><span data-stu-id="9f8d8-139">[Add a VM with artifacts to a lab](https://azure.microsoft.com/resources/videos/how-to-create-vms-with-artifacts-in-a-devtest-lab/).</span></span>

