---
title: "Azure VM을 기반으로 Azure RemoteApp 이미지 만들기 | Microsoft 문서"
description: "Azure 가상 컴퓨터를 시작하여 Azure RemoteApp에 대한 이미지를 만드는 방법에 대해 알아봅니다."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: d41583ef-6cd8-4115-8dcb-b2cd5b3d301a
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: ee64b86835af8e6237cddcd8acc779fc6dac8214
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-azure-remoteapp-image-based-on-an-azure-virtual-machine"></a><span data-ttu-id="9972d-103">Azure 가상 컴퓨터를 기반으로 Azure RemoteApp 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="9972d-103">Create a Azure RemoteApp image based on an Azure virtual machine</span></span>
> [!IMPORTANT]
> <span data-ttu-id="9972d-104">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9972d-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="9972d-105">자세한 내용은 [알림](https://go.microsoft.com/fwlink/?linkid=821148) 을 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="9972d-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="9972d-106">Azure 가상 컴퓨터에서 Azure RemoteApp 이미지(컬렉션에서 공유하는 앱을 포함)를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9972d-106">You can create Azure RemoteApp images (which hold the apps you share in your collection) from an Azure virtual machine.</span></span> <span data-ttu-id="9972d-107">Azure RemoteApp 이미지 요구 사항을 모두 충족하는 Azure VM 이미지 갤러리에 추가한 가상 컴퓨터 이미지를 사용하도록 선택할 수도 있습니다. 원하는 경우 해당 VM 이미지를 자신만의 VM을 위한 시작점으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9972d-107">You could also choose to use a virtual machine image we added to the Azure VM image gallery that meets all the Azure RemoteApp image requirements - you can use that VM image as a starting point for your own VM, if you want.</span></span> <span data-ttu-id="9972d-108">"Windows Server 원격 데스크톱 세션 호스트" 이미지를 라이브러리에서 찾으면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9972d-108">Just look for the "Windows Server Remote Desktop Session Host" image in the library.</span></span>

<span data-ttu-id="9972d-109">Azure VM을 기반으로 자신만의 이미지를 만드는 단계는 두 가지입니다. 이미지를 만든 다음 Azure VM 라이브러리에서 Azure RemoteApp으로 업로드하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9972d-109">There are two steps to create your own image based on an Azure VM - create the image and then upload it from the Azure VM library to Azure RemoteApp.</span></span>

## <a name="create-a-custom-image-based-on-an-azure-vm"></a><span data-ttu-id="9972d-110">Azure VM을 기반으로 사용자 지정 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="9972d-110">Create a custom image based on an Azure VM</span></span>
<span data-ttu-id="9972d-111">Azure VM을 기반으로 이미지를 만들려면 이 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9972d-111">Use these steps to create an image based on an Azure VM.</span></span>

1. <span data-ttu-id="9972d-112">Azure 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9972d-112">Create an Azure virtual machine.</span></span> <span data-ttu-id="9972d-113">Azure 가상 컴퓨터 이미지 갤러리에서 "Windows Server 원격 데스크톱 세션 호스트" 또는 "Microsoft Office 365 ProPlus가 있는 Windows Server 원격 데스크톱 세션 호스트" 이미지를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9972d-113">You can use the "Windows Server Remote Desktop Session Host" or the "Windows Server Remote Desktop Session Host with Microsoft Office 365 ProPlus" image from the Azure virtual machine image gallery.</span></span> <span data-ttu-id="9972d-114">이 이미지는 Azure RemoteApp 템플릿 이미지 요구 사항을 모두 충족합니다.</span><span class="sxs-lookup"><span data-stu-id="9972d-114">This image meets all the Azure RemoteApp template image requirements.</span></span>
   
    <span data-ttu-id="9972d-115">자세한 내용은 [Windows를 실행하는 VM 만들기](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9972d-115">For details, see [Create a VM running Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
2. <span data-ttu-id="9972d-116">VM에 연결하고 RemoteApp을 통해 공유하려는 앱을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="9972d-116">Connect to the VM and install and configure the apps that you want to share through RemoteApp.</span></span> <span data-ttu-id="9972d-117">앱에 필요한 모든 추가 Windows 구성을 수행할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9972d-117">Make sure to perform any additional Windows configurations required by your apps.</span></span>
   
    <span data-ttu-id="9972d-118">자세한 내용은 [Windows Server를 실행하는 가상 컴퓨터에 로그온하는 방법](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9972d-118">For details, see [How to Log on to a Virtual Machine Running Windows Server](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>
3. <span data-ttu-id="9972d-119">Windows Server 원격 데스크톱 세션 호스트 이미지 중 하나를 사용하는 경우 VM이 RemoteApp 사전 요구 사항을 충족하는지 확인하는 유효성 검사 스크립트가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9972d-119">If you are using one of the Windows Server Remote Desktop Session Host images, there is an included validation script that will ensure your VM meets the RemoteApp pre-reqs.</span></span> <span data-ttu-id="9972d-120">스크립트를 실행하려면 바탕 화면에서 **ValidateRemoteAppImage** 를 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9972d-120">To run script, double-click **ValidateRemoteAppImage** on the desktop.</span></span> <span data-ttu-id="9972d-121">다음 단계를 진행하기 전에 스크립트에서 보고한 모든 오류가 해결되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9972d-121">Ensure that all errors reported by the script are fixed before proceeding to the next step.</span></span>
4. <span data-ttu-id="9972d-122">SYSPREP가 일반화되고 이미지를 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="9972d-122">SYSPREP generalize and capture the image.</span></span> <span data-ttu-id="9972d-123">지침에 대해서는 [템플릿으로 사용할 Windows Virtual Machine를 캡처하는 방법](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9972d-123">See [How to Capture a Windows Virtual Machine to Use as a Template](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) for instructions.</span></span>

## <a name="import-the-image-into-the-azure-remoteapp-image-library"></a><span data-ttu-id="9972d-124">Azure RemoteApp 이미지 라이브러리로 이미지 가져오기</span><span class="sxs-lookup"><span data-stu-id="9972d-124">Import the image into the Azure RemoteApp image library</span></span>
<span data-ttu-id="9972d-125">다음 단계를 사용하여 새 이미지를 Azure RemoteApp으로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="9972d-125">Use these steps to import the new image into Azure RemoteApp:</span></span>

1. <span data-ttu-id="9972d-126">**템플릿 이미지** 탭에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9972d-126">In the **Template Images** tab:</span></span>
   
   * <span data-ttu-id="9972d-127">기존 이미지가 없는 경우 **템플릿 이미지를 업로드하거나 가져오기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9972d-127">If you have no existing images, click **Upload or Import a Template Image**.</span></span>
   * <span data-ttu-id="9972d-128">하나 이상의 이미지가 이미 있는 경우 **+** 를 클릭하여 새 이미지를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9972d-128">If you have at least one image already, click **+** to add a new image.</span></span>
2. <span data-ttu-id="9972d-129">**Virtual Machines에서 이미지 가져오기** 라이브러리를 선택한 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9972d-129">Select **Import an image from your Virtual Machines** library, and then click **Next**.</span></span>
3. <span data-ttu-id="9972d-130">다음 페이지에서 목록에서 사용자 지정 이미지를 선택하고 이미지를 만들 때 나열된 단계를 수행했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9972d-130">On the next page, select your custom image from the list and confirm that you followed the steps listed when you created your image.</span></span> <span data-ttu-id="9972d-131">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="9972d-131">Click **Next**.</span></span>
4. <span data-ttu-id="9972d-132">새 RemoteApp 이미지에 대한 이름을 입력하고 위치를 선택한 다음 확인 표시를 클릭하여 가져오기 프로세스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="9972d-132">Enter a name for the new RemoteApp image and pick the location, then click the checkmark to start the import process.</span></span>

> [!NOTE]
> <span data-ttu-id="9972d-133">Azure 가상 컴퓨터에서 지원하는 모든 Azure 위치에서 Azure RemoteApp에서 지원하는 모든 Azure 위치로 이미지를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9972d-133">You can import images from any Azure location supported by Azure Virtual Machines to any Azure location supported by Azure RemoteApp.</span></span> <span data-ttu-id="9972d-134">가져오기는 위치에 따라 최대 25분까지 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9972d-134">Depending on the locations the import can take up to 25 minutes.</span></span>
> 
> 

<span data-ttu-id="9972d-135">이제 필요에 따라 [클라우드](remoteapp-create-cloud-deployment.md) 컬렉션 또는 [하이브리드](remoteapp-create-hybrid-deployment.md), 컬렉션을 새로 만들 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9972d-135">Now you are ready to create your new collection, either a [cloud](remoteapp-create-cloud-deployment.md) collection or [hybrid](remoteapp-create-hybrid-deployment.md), depending on your needs.</span></span>

