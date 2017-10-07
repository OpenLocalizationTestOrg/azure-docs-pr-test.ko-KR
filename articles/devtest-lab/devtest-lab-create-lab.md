---
title: "Azure DevTest Labs에 랩 aaaCreate | Microsoft Docs"
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
ms.openlocfilehash: 2ec5498f10e0cc06a196a71e319e340937abb1a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="88fbc-103">Azure DevTest Labs에서 랩 만들기</span><span class="sxs-lookup"><span data-stu-id="88fbc-103">Create a lab in Azure DevTest Labs</span></span>
<span data-ttu-id="88fbc-104">Azure DevTest Labs에 랩은 제한 및 할당량을 지정 하 여 해당 리소스를 관리 하는 더 나은 수 있는 가상 컴퓨터 (Vm) 등의 리소스 그룹을 포함 하는 hello 인프라 합니다.</span><span class="sxs-lookup"><span data-stu-id="88fbc-104">A lab in Azure DevTest Labs is hello infrastructure that encompasses a group of resources, such as Virtual Machines (VMs), that lets you better manage those resources by specifying limits and quotas.</span></span> <span data-ttu-id="88fbc-105">이 문서는 hello hello Azure 포털을 사용 하 여 랩을 만드는 과정을 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="88fbc-105">This article walks you through hello process of creating a lab using hello Azure portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="88fbc-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="88fbc-106">Prerequisites</span></span>
<span data-ttu-id="88fbc-107">랩 toocreate 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="88fbc-107">toocreate a lab, you need:</span></span>

* <span data-ttu-id="88fbc-108">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="88fbc-108">An Azure subscription.</span></span> <span data-ttu-id="88fbc-109">Azure 구입 옵션에 대 한 toolearn 참조 [어떻게 toobuy Azure](https://azure.microsoft.com/pricing/purchase-options/) 또는 [무료 1 개월 평가판](https://azure.microsoft.com/pricing/free-trial/)합니다.</span><span class="sxs-lookup"><span data-stu-id="88fbc-109">toolearn about Azure purchase options, see [How toobuy Azure](https://azure.microsoft.com/pricing/purchase-options/) or [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="88fbc-110">Hello 구독 toocreate hello 랩의 hello 소유자 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="88fbc-110">You must be hello owner of hello subscription toocreate hello lab.</span></span>

## <a name="steps-toocreate-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="88fbc-111">단계 toocreate Azure DevTest Labs에 랩</span><span class="sxs-lookup"><span data-stu-id="88fbc-111">Steps toocreate a lab in Azure DevTest Labs</span></span>
<span data-ttu-id="88fbc-112">단계를 수행 하는 hello를 방법을 toouse hello Azure 포털 toocreate Azure DevTest Labs에 랩 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="88fbc-112">hello following steps illustrate how toouse hello Azure portal toocreate a lab in Azure DevTest Labs.</span></span> 

1. <span data-ttu-id="88fbc-113">Toohello 로그인 [Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)합니다.</span><span class="sxs-lookup"><span data-stu-id="88fbc-113">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="88fbc-114">Hello 왼쪽에 hello 주 메뉴에서 선택 **더 서비스** (하단의 hello hello 목록).</span><span class="sxs-lookup"><span data-stu-id="88fbc-114">From hello main menu on hello left side, select **More Services** (at hello bottom of hello list).</span></span>

    ![추가 서비스 메뉴 옵션](./media/devtest-lab-create-lab/more-services-menu-option.png)

1. <span data-ttu-id="88fbc-116">사용 가능한 서비스는 hello 목록에서 **DevTest Labs**합니다.</span><span class="sxs-lookup"><span data-stu-id="88fbc-116">From hello list of available services, **DevTest Labs**.</span></span>
1. <span data-ttu-id="88fbc-117">Hello에 **DevTest Labs** 블레이드를 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="88fbc-117">On hello **DevTest Labs** blade, select **Add**.</span></span>
   
    ![랩 추가](./media/devtest-lab-create-lab/add-lab-button.png)

1. <span data-ttu-id="88fbc-119">Hello에 **DevTest Lab 만들** 블레이드:</span><span class="sxs-lookup"><span data-stu-id="88fbc-119">On hello **Create a DevTest Lab** blade:</span></span>
   
    1. <span data-ttu-id="88fbc-120">입력 한 **랩 이름이** hello 새 랩에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="88fbc-120">Enter a **Lab Name** for hello new lab.</span></span>
    2. <span data-ttu-id="88fbc-121">선택 hello **구독** hello 랩에서 tooassociate 합니다.</span><span class="sxs-lookup"><span data-stu-id="88fbc-121">Select hello **Subscription** tooassociate with hello lab.</span></span>
    3. <span data-ttu-id="88fbc-122">선택 된 **위치** 어떤 toostore hello 랩에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="88fbc-122">Select a **Location** in which toostore hello lab.</span></span>
    4. <span data-ttu-id="88fbc-123">선택 **자동 종료** toospecify tooenable--hello 매개 변수를 정의할 경우 hello 자동 종료 하 고 모든 hello 랩 Vm의 합니다.</span><span class="sxs-lookup"><span data-stu-id="88fbc-123">Select **Auto-shutdown** toospecify if you want tooenable - and define hello parameters for - hello automatic shutting down of all hello lab's VMs.</span></span> <span data-ttu-id="88fbc-124">hello 자동 종료 기능은 주로 VM hello 할 때를 지정할 수는 그에 따라 비용 절감 기능 tooautomatically 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="88fbc-124">hello auto-shutdown feature is mainly a cost-saving feature whereby you can specify when you want hello VM tooautomatically be shut down.</span></span> <span data-ttu-id="88fbc-125">Hello 랩 hello 문서에서 설명 하는 hello 단계를 수행 하 여 만든 후 자동 종료 설정을 변경할 수 있습니다 [Azure DevTest Labs에 랩에 대 한 모든 정책을 관리](./devtest-lab-set-lab-policy.md#set-auto-shutdown)합니다.</span><span class="sxs-lookup"><span data-stu-id="88fbc-125">You can change auto-shutdown settings after creating hello lab by following hello steps outlined in hello article, [Manage all policies for a lab in Azure DevTest Labs](./devtest-lab-set-lab-policy.md#set-auto-shutdown).</span></span>
    5. <span data-ttu-id="88fbc-126">선택 **Pin tooDashboard** hello 포털 대시보드에서 hello 랩 tooappear의 바로 가기에 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88fbc-126">Select **Pin tooDashboard** if you want a shortcut of hello lab tooappear on hello portal dashboard.</span></span>
    6. <span data-ttu-id="88fbc-127">선택 **자동화 옵션** tooget Azure 리소스 관리자 템플릿을 구성 자동화에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="88fbc-127">Select **Automation options** tooget Azure Resource Manager templates for configuration automation.</span></span> 
    7. <span data-ttu-id="88fbc-128">**만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="88fbc-128">Select **Create**.</span></span> <span data-ttu-id="88fbc-129">선택한 후 **만들기**, hello **DevTest Labs** 블레이드를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="88fbc-129">After selecting **Create**, hello **DevTest Labs** blade displays.</span></span> <span data-ttu-id="88fbc-130">Hello를 시청 하 여 hello 랩 만들기 프로세스의 hello 상태를 모니터링할 수 있습니다 **알림** 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="88fbc-130">You can monitor hello status of hello lab creation process by watching hello **Notifications** area.</span></span> <span data-ttu-id="88fbc-131">완료 되 면 hello 페이지 toosee 새로 만든 hello 랩을 연구소 hello 목록에서 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="88fbc-131">Once completed, refresh hello page toosee hello newly created lab in hello list of labs.</span></span>  
    
    ![랩 블레이드 만들기](./media/devtest-lab-create-lab/create-devtestlab-blade.png)

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="88fbc-133">다음 단계</span><span class="sxs-lookup"><span data-stu-id="88fbc-133">Next steps</span></span>
<span data-ttu-id="88fbc-134">랩 만들었으면 다음 몇 가지 단계 tooconsider 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="88fbc-134">Once you've created your lab, here are some next steps tooconsider:</span></span>

* <span data-ttu-id="88fbc-135">[보안 액세스 tooa 랩](devtest-lab-add-devtest-user.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="88fbc-135">[Secure access tooa lab](devtest-lab-add-devtest-user.md).</span></span>
* <span data-ttu-id="88fbc-136">[랩 정책 설정](devtest-lab-set-lab-policy.md).</span><span class="sxs-lookup"><span data-stu-id="88fbc-136">[Set lab policies](devtest-lab-set-lab-policy.md).</span></span>
* <span data-ttu-id="88fbc-137">[랩 템플릿 만들기](devtest-lab-create-template.md).</span><span class="sxs-lookup"><span data-stu-id="88fbc-137">[Create a lab template](devtest-lab-create-template.md).</span></span>
* <span data-ttu-id="88fbc-138">[VM에 대한 사용자 지정 아티팩트  만들기](devtest-lab-artifact-author.md).</span><span class="sxs-lookup"><span data-stu-id="88fbc-138">[Create custom artifacts for your VMs](devtest-lab-artifact-author.md).</span></span>
* <span data-ttu-id="88fbc-139">[Tooa 랩 아티팩트를 사용 하 여 VM을 추가](https://azure.microsoft.com/resources/videos/how-to-create-vms-with-artifacts-in-a-devtest-lab/)합니다.</span><span class="sxs-lookup"><span data-stu-id="88fbc-139">[Add a VM with artifacts tooa lab](https://azure.microsoft.com/resources/videos/how-to-create-vms-with-artifacts-in-a-devtest-lab/).</span></span>

