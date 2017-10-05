---
title: "Azure DevTest Labs에서 Azure Marketplace 이미지 설정 구성 | Microsoft 문서"
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
ms.openlocfilehash: 5f888c9d92a9164cc7d3d1aed66c29a724b365d7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="configure-azure-marketplace-image-settings-in-azure-devtest-labs"></a><span data-ttu-id="bad33-103">Azure DevTest Labs에서 Azure 마켓플레이스 이미지 설정 구성</span><span class="sxs-lookup"><span data-stu-id="bad33-103">Configure Azure Marketplace image settings in Azure DevTest Labs</span></span>
<span data-ttu-id="bad33-104">DevTest Lab에서는 Azure 마켓플레이스 이미지를 랩에서 사용하도록 구성한 방법에 따라 Azure 마켓플레이스 이미지를 기준으로 VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bad33-104">DevTest Labs supports creating VMs based on Azure Marketplace images depending on how you have configured Azure Marketplace images to be used in your lab.</span></span> <span data-ttu-id="bad33-105">이 문서에서는 랩에서 VM을 만들 때 사용할 수 있는 Azure 마켓플레이스 이미지(있는 경우)를 지정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bad33-105">This article shows you how to specify which, if any, Azure Marketplace images can be used when creating VMs in a lab.</span></span> <span data-ttu-id="bad33-106">이 경우 팀은 필요한 Marketplace 이미지에만 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bad33-106">This ensures that your team only has access to the Marketplace images they need.</span></span> 

## <a name="select-which-azure-marketplace-images-are-allowed-when-creating-a-vm"></a><span data-ttu-id="bad33-107">VM을 만들 때 허용되는 Azure 마켓플레이스 이미지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bad33-107">Select which Azure Marketplace images are allowed when creating a VM</span></span>
1. <span data-ttu-id="bad33-108">[Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="bad33-108">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="bad33-109">**추가 서비스**를 선택한 후 목록에서 **DevTest Labs**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bad33-109">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="bad33-110">랩 목록에서 원하는 랩을 탭합니다.</span><span class="sxs-lookup"><span data-stu-id="bad33-110">From the list of labs, select the desired lab.</span></span> 
4. <span data-ttu-id="bad33-111">랩의 블레이드에서 **구성 및 정책**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bad33-111">On the lab's blade, select **Configuration and policies**.</span></span>
5. <span data-ttu-id="bad33-112">랩의 **구성 및 정책** 블레이드에 있는 **가상 컴퓨터 기본**에서 **Marketplace 이미지**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bad33-112">On lab's **Configuration and policies** blade under **Virtual Machine Bases**, select **Marketplace images**.</span></span>
6. <span data-ttu-id="bad33-113">모든 정규화된 Azure 마켓플레이스 이미지를 새 VM의 기반으로 사용할 수 있게 할지 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="bad33-113">Specify whether you want all the qualified Azure Marketplace images to be available for use as a base of a new VM.</span></span> <span data-ttu-id="bad33-114">**예**를 선택하는 경우 다음 조건을 모두 충족하는 모든 Azure 마켓플레이스 이미지가 랩에서 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="bad33-114">If you select **Yes**, then all the Azure Marketplace images that meet all the following criteria are allowed in the lab:</span></span>
   
   * <span data-ttu-id="bad33-115">이 이미지는 단일 VM을 만듭니다. **그리고**</span><span class="sxs-lookup"><span data-stu-id="bad33-115">The image creates a single VM, **and**</span></span>
   * <span data-ttu-id="bad33-116">이 이미지는 Azure Resource Manager를 사용하여 VM을 프로비전합니다. **그리고**</span><span class="sxs-lookup"><span data-stu-id="bad33-116">The image uses Azure Resource Manager to provision VMs, **and**</span></span>
   * <span data-ttu-id="bad33-117">이 이미지는 추가 라이선스 계획을 구입하지 않아도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bad33-117">The image doesn't require purchasing an extra licensing plan</span></span>
     
    <span data-ttu-id="bad33-118">이미지를 허용하지 않거나 사용할 수 있는 이미지를 지정하려면 **아니요**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bad33-118">If you want no images to be allowed, or you want to specify which images can be used, select **No**.</span></span>
     
     ![모든 마켓플레이스 이미지를 VM에 대한 기본 이미지로 사용할 수 있도록 허용하는 옵션](./media/devtest-lab-configure-marketplace-images/allow-all-marketplace-images.png)
7. <span data-ttu-id="bad33-120">이전 단계에서 **아니요**를 선택하는 경우 **허용된 이미지/모두 선택** 확인란이 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="bad33-120">If you select **No** to the previous step, the **Allowed images/Select all** checkbox is enabled.</span></span> 
   <span data-ttu-id="bad33-121">검색 상자와 함께 이 옵션을 사용하면 목록에 표시된 모든 항목을 빠르게 선택하거나 선택 취소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bad33-121">You can use this option together with the search box to quickly select or deselect all the items displayed in the list.</span></span>
   * <span data-ttu-id="bad33-122">각 이미지의 해당 확인란을 선택하여 VM 만들기를 개별적으로 허용하려는 Azure Marketplace 이미지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bad33-122">Select the Azure Marketplace images you want to allow for VM creation individually by checking each image's corresponding checkbox.</span></span>
   * <span data-ttu-id="bad33-123">랩에서 Azure 마켓플레이스 이미지를 사용하도록 허용하지 않으려면 목록에서 아무 것도 선택하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bad33-123">Select nothing from the list if you don't want to allow any Azure Marketplace images to be used in the lab.</span></span>
   
    ![VM에 대한 기본 이미지로 사용할 수 있는 Azure 마켓플레이스 이미지를 지정할 수 있습니다.](./media/devtest-lab-configure-marketplace-images/select-marketplace-images.png)

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="bad33-125">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bad33-125">Next steps</span></span>
<span data-ttu-id="bad33-126">VM을 만들 때 Azure Marketplace 이미지를 허용하는 방법을 구성했으면 다음 단계는 [VM을 랩에 추가](devtest-lab-add-vm-with-artifacts.md)하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bad33-126">Once you have configured how Azure Marketplace images are allowed when creating a VM, the next step is to [add a VM to your lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

