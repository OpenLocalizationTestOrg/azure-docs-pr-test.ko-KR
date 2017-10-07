---
title: "DevTest Labs Azure에서에서 Azure 마켓플레이스 이미지 설정 aaaConfigure | Microsoft Docs"
description: "Azure DevTest Labs에서 VM을 만들 때 사용할 수 있는 Azure 마켓플레이스 이미지 구성"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 804c6af2-17e9-4320-af3a-f454bd398379
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/25/2016
ms.author: tarcher
ms.openlocfilehash: bb4b7f1c0cbe967bee724f7ee20f64f8c4ea58ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-marketplace-image-settings-in-azure-devtest-labs"></a><span data-ttu-id="bf012-103">Azure DevTest Labs에서 Azure 마켓플레이스 이미지 설정 구성</span><span class="sxs-lookup"><span data-stu-id="bf012-103">Configure Azure Marketplace image settings in Azure DevTest Labs</span></span>
<span data-ttu-id="bf012-104">DevTest Labs 랩에서 사용 되는 Azure 마켓플레이스 이미지 toobe을 어떻게 구성 했는지에 따라 Azure 마켓플레이스 이미지를 기반으로 만드는 Vm을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf012-104">DevTest Labs supports creating VMs based on Azure Marketplace images depending on how you have configured Azure Marketplace images toobe used in your lab.</span></span> <span data-ttu-id="bf012-105">이 문서에서는 Azure 마켓플레이스 이미지 될 수 있는 경우 있는 toospecify 랩에서 Vm을 만들 때 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf012-105">This article shows you how toospecify which, if any, Azure Marketplace images can be used when creating VMs in a lab.</span></span> <span data-ttu-id="bf012-106">이렇게 하면 팀에만 필요한 액세스 toohello 마켓플레이스 이미지에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf012-106">This ensures that your team only has access toohello Marketplace images they need.</span></span> 

## <a name="select-which-azure-marketplace-images-are-allowed-when-creating-a-vm"></a><span data-ttu-id="bf012-107">VM을 만들 때 허용되는 Azure 마켓플레이스 이미지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bf012-107">Select which Azure Marketplace images are allowed when creating a VM</span></span>
1. <span data-ttu-id="bf012-108">Toohello 로그인 [Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)합니다.</span><span class="sxs-lookup"><span data-stu-id="bf012-108">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="bf012-109">선택 **더 서비스**를 선택한 후 **DevTest Labs** hello 목록에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf012-109">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="bf012-110">랩의 hello 목록에서 원하는 랩 hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf012-110">From hello list of labs, select hello desired lab.</span></span> 
4. <span data-ttu-id="bf012-111">Hello 랩 블레이드에서 선택 **구성 및 정책**합니다.</span><span class="sxs-lookup"><span data-stu-id="bf012-111">On hello lab's blade, select **Configuration and policies**.</span></span>
5. <span data-ttu-id="bf012-112">랩의 **구성 및 정책** 블레이드에 있는 **가상 컴퓨터 기본**에서 **Marketplace 이미지**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bf012-112">On lab's **Configuration and policies** blade under **Virtual Machine Bases**, select **Marketplace images**.</span></span>
6. <span data-ttu-id="bf012-113">새 VM의 기본으로 사용 하기 위해 사용할 수 있는 정규화 된 Azure 마켓플레이스 이미지 toobe hello 모두 사용할지를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf012-113">Specify whether you want all hello qualified Azure Marketplace images toobe available for use as a base of a new VM.</span></span> <span data-ttu-id="bf012-114">선택 하는 경우 **예**, 다음 모든 hello Azure 마켓플레이스 이미지 모든 hello 다음 조건을 충족 하는 랩에서 허용 hello:</span><span class="sxs-lookup"><span data-stu-id="bf012-114">If you select **Yes**, then all hello Azure Marketplace images that meet all hello following criteria are allowed in hello lab:</span></span>
   
   * <span data-ttu-id="bf012-115">hello 이미지 만듭니다는 단일 VM **및**</span><span class="sxs-lookup"><span data-stu-id="bf012-115">hello image creates a single VM, **and**</span></span>
   * <span data-ttu-id="bf012-116">Azure 리소스 관리자 tooprovision Vm을 사용 하 여 hello 이미지 **및**</span><span class="sxs-lookup"><span data-stu-id="bf012-116">hello image uses Azure Resource Manager tooprovision VMs, **and**</span></span>
   * <span data-ttu-id="bf012-117">추가 라이선스 계획 구입 hello 이미지 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bf012-117">hello image doesn't require purchasing an extra licensing plan</span></span>
     
    <span data-ttu-id="bf012-118">를 사용할 수 없는 이미지 toobe 싶거나 toospecify 선택, 사용할 수 있는 이미지를 원하는 **아니요**합니다.</span><span class="sxs-lookup"><span data-stu-id="bf012-118">If you want no images toobe allowed, or you want toospecify which images can be used, select **No**.</span></span>
     
     ![Vm에 대 한 기본 이미지로 옵션 tooallow 모든 마켓플레이스 이미지 toobe 사용](./media/devtest-lab-configure-marketplace-images/allow-all-marketplace-images.png)
7. <span data-ttu-id="bf012-120">선택 하는 경우 **아니요** toohello 이전 단계 hello **허용 이미지/선택 모든** 확인란을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf012-120">If you select **No** toohello previous step, hello **Allowed images/Select all** checkbox is enabled.</span></span> 
   <span data-ttu-id="bf012-121">검색 상자 tooquickly 선택 hello와 함께이 옵션을 사용 하거나 hello 목록에 표시 되는 모든 hello 항목은 선택 취소 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf012-121">You can use this option together with hello search box tooquickly select or deselect all hello items displayed in hello list.</span></span>
   * <span data-ttu-id="bf012-122">원하는 tooallow VM 만들기에 개별적으로 각 이미지의 해당 확인란을 선택 하 여 hello Azure 마켓플레이스 이미지를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf012-122">Select hello Azure Marketplace images you want tooallow for VM creation individually by checking each image's corresponding checkbox.</span></span>
   * <span data-ttu-id="bf012-123">Tooallow hello 랩에서 사용 되는 모든 Azure 마켓플레이스 이미지 toobe 않으려는 경우 아무 hello 목록에서 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf012-123">Select nothing from hello list if you don't want tooallow any Azure Marketplace images toobe used in hello lab.</span></span>
   
    ![VM에 대한 기본 이미지로 사용할 수 있는 Azure 마켓플레이스 이미지를 지정할 수 있습니다.](./media/devtest-lab-configure-marketplace-images/select-marketplace-images.png)

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="bf012-125">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bf012-125">Next steps</span></span>
<span data-ttu-id="bf012-126">VM을 만들 때 Azure 마켓플레이스 이미지는 허용 하는 방법을 구성 되 면 hello 다음 단계는 너무[추가 VM tooyour 랩](devtest-lab-add-vm-with-artifacts.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="bf012-126">Once you have configured how Azure Marketplace images are allowed when creating a VM, hello next step is too[add a VM tooyour lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

