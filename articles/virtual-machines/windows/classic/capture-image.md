---
title: "Azure Windows VM의 이미지 캡처 | Microsoft Docs"
description: "클래식 배포 모델을 사용하여 만든 Azure Windows 가상 컴퓨터의 이미지를 캡처합니다."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: a5986eac-4cf3-40bd-9b79-7c811806b880
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: 6032263848c469ce2f416306e5c91c29f4cb30e4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="capture-an-image-of-an-azure-windows-virtual-machine-created-with-the-classic-deployment-model"></a><span data-ttu-id="58647-103">클래식 배포 모델을 사용하여 만든 Azure Windows 가상 컴퓨터의 이미지를 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="58647-103">Capture an image of an Azure Windows virtual machine created with the classic deployment model.</span></span>
> [!IMPORTANT]
> <span data-ttu-id="58647-104">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58647-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="58647-105">이 문서에서는 클래식 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="58647-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="58647-106">새로운 배포는 대부분 리소스 관리자 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="58647-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="58647-107">Resource Manager 모델 정보는 [Azure에서 일반화된 VM의 관리되는 이미지 캡처](../capture-image-resource.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="58647-107">For Resource Manager model information, see [Capture a managed image of a generalized VM in Azure](../capture-image-resource.md).</span></span>

<span data-ttu-id="58647-108">이 문서에서는 Windows가 실행되는 Azure 가상 컴퓨터를 캡처하여 다른 가상 컴퓨터를 만들 때 이미지로 사용하는 방법을 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="58647-108">This article shows you how to capture an Azure virtual machine running Windows so you can use it as an image to create other virtual machines.</span></span> <span data-ttu-id="58647-109">이 이미지에는 OS 디스크를 비롯해 가상 컴퓨터에 연결되는 모든 데이터 디스크가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="58647-109">This image includes the operating system disk and any data disks that are attached to the virtual machine.</span></span> <span data-ttu-id="58647-110">네트워킹 구성은 포함되지 않으므로, 이미지를 사용하는 다른 가상 컴퓨터를 만들 때 네트워크 구성을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="58647-110">It doesn't include networking configurations, so you'll need to set up network configurations when you create the other virtual machines that use the image.</span></span>

<span data-ttu-id="58647-111">Azure에서는 모든 Azure 서비스를 볼 때 나열된 **계산** 서비스인 **VM 이미지(클래식)** 아래에 이미지를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="58647-111">Azure stores the image under **VM images (classic)**, a **Compute** service that is listed when you view all the Azure services.</span></span> <span data-ttu-id="58647-112">사용자가 업로드한 모든 이미지도 이 위치에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="58647-112">This is the same place where any images you've uploaded are stored.</span></span> <span data-ttu-id="58647-113">이미지에 대한 자세한 내용은 [가상 컴퓨터 이미지 정보](about-images.md?toc=%2fazure%2fvirtual-machines%2fWindows%2fclassic%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="58647-113">For details about images, see [About images for virtual machines](about-images.md?toc=%2fazure%2fvirtual-machines%2fWindows%2fclassic%2ftoc.json).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="58647-114">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="58647-114">Before you begin</span></span>
<span data-ttu-id="58647-115">이러한 단계는 이미 Azure 가상 컴퓨터를 만들었으며 데이터 디스크 연결을 비롯해 운영 체제 구성을 완료했다는 것을 전제로 합니다.</span><span class="sxs-lookup"><span data-stu-id="58647-115">These steps assume that you've already created an Azure virtual machine and configured the operating system, including attaching any data disks.</span></span> <span data-ttu-id="58647-116">아직 수행하지 않은 경우 가상 컴퓨터를 만들고 준비하는 정보는 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="58647-116">If you haven't done this yet, see the following articles for information on creating and preparing the virtual machine:</span></span>

* [<span data-ttu-id="58647-117">이미지에서 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="58647-117">Create a virtual machine from an image</span></span>](createportal.md)
* [<span data-ttu-id="58647-118">가상 컴퓨터에 데이터 디스크를 연결하는 방법</span><span class="sxs-lookup"><span data-stu-id="58647-118">How to attach a data disk to a virtual machine</span></span>](attach-disk.md)
* <span data-ttu-id="58647-119">서버 역할이 Sysprep에서 지원되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="58647-119">Make sure the server roles are supported with Sysprep.</span></span> <span data-ttu-id="58647-120">자세한 내용은 [서버 역할에 대한 Sysprep 지원](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="58647-120">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span></span>

> [!WARNING]
> <span data-ttu-id="58647-121">이 프로세스는 캡처된 후 원래의 가상 컴퓨터를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="58647-121">This process deletes the original virtual machine after it's captured.</span></span>
>
>

<span data-ttu-id="58647-122">Azure Virtual Machine의 이미지를 캡처하기 전에 대상 가상 컴퓨터를 백업하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="58647-122">Prior to capturing an image of an Azure virtual machine, it is recommended the target virtual machine be backed up.</span></span> <span data-ttu-id="58647-123">Azure 백업을 사용하여 Azure 가상 컴퓨터를 백업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58647-123">Azure virtual machines can be backed up using Azure Backup.</span></span> <span data-ttu-id="58647-124">자세한 내용은 [Azure 가상 컴퓨터 백업](../../../backup/backup-azure-vms.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="58647-124">For details, see [Back up Azure virtual machines](../../../backup/backup-azure-vms.md).</span></span> <span data-ttu-id="58647-125">다른 솔루션은 인증된 파트너에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58647-125">Other solutions are available from certified partners.</span></span> <span data-ttu-id="58647-126">무엇이 현재 사용 가능한지 알아보려면, Azure 마켓플레이스를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="58647-126">To find out what’s currently available, search the Azure Marketplace.</span></span>

## <a name="capture-the-virtual-machine"></a><span data-ttu-id="58647-127">가상 컴퓨터 캡처</span><span class="sxs-lookup"><span data-stu-id="58647-127">Capture the virtual machine</span></span>
1. <span data-ttu-id="58647-128">[Azure Portal](http://portal.azure.com)에서 가상 컴퓨터에 **연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="58647-128">In the [Azure portal](http://portal.azure.com), **Connect** to the virtual machine.</span></span> <span data-ttu-id="58647-129">지침은 [Windows Server를 실행하여 가상 컴퓨터에 로그인하는 방법][How to sign in to a virtual machine running Windows Server]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="58647-129">For instructions, see [How to sign in to a virtual machine running Windows Server][How to sign in to a virtual machine running Windows Server].</span></span>
2. <span data-ttu-id="58647-130">관리자로 명령 프롬프트 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="58647-130">Open a Command Prompt window as an administrator.</span></span>
3. <span data-ttu-id="58647-131">디렉터리를 `%windir%\system32\sysprep`로 변경한 후 sysprep.exe를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="58647-131">Change the directory to `%windir%\system32\sysprep`, and then run sysprep.exe.</span></span>
4. <span data-ttu-id="58647-132">**시스템 준비 도구** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="58647-132">The **System Preparation Tool** dialog box appears.</span></span> <span data-ttu-id="58647-133">다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="58647-133">Do the following:</span></span>

   * <span data-ttu-id="58647-134">**시스템 정리 작업**에서 **시스템 OOBE(첫 실행 경험) 입력**을 선택하고 **일반화**를 선택했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="58647-134">In **System Cleanup Action**, select **Enter System Out-of-Box Experience (OOBE)** and make sure that **Generalize** is checked.</span></span> <span data-ttu-id="58647-135">Sysprep 사용에 대한 자세한 내용은 [Sysprep 사용 방법: 소개][How to Use Sysprep: An Introduction]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="58647-135">For more information about using Sysprep, see [How to Use Sysprep: An Introduction][How to Use Sysprep: An Introduction].</span></span>
   * <span data-ttu-id="58647-136">**종료 옵션**에서 **종료**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="58647-136">In **Shutdown Options**, select **Shutdown**.</span></span>
   * <span data-ttu-id="58647-137">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="58647-137">Click **OK**.</span></span>

   ![Sysprep 실행](./media/capture-image/SysprepGeneral.png)
5. <span data-ttu-id="58647-139">Sysprep을 실행하면 가상 컴퓨터가 종료되고 Azure Portal의 가상 컴퓨터 상태가 **중지됨**으로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="58647-139">Sysprep shuts down the virtual machine, which changes the status of the virtual machine in the Azure portal to **Stopped**.</span></span>
6. <span data-ttu-id="58647-140">Azure Portal에서 **가상 컴퓨터(클래식)**를 클릭한 후 캡처하려는 가상 컴퓨터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="58647-140">In the Azure portal, click **Virtual Machines (classic)** and select the virtual machine you want to capture.</span></span> <span data-ttu-id="58647-141">**VM 이미지(클래식)** 그룹은 **추가 서비스**를 볼 때 **계산** 아래에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="58647-141">The **VM images (classic)** group is listed under **Compute** when you view **More services**.</span></span>

7. <span data-ttu-id="58647-142">명령 모음에서 **캡처**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="58647-142">On the command bar, click **Capture**.</span></span>

   ![가상 컴퓨터 캡처](./media/capture-image/CaptureVM.png)

   <span data-ttu-id="58647-144">**가상 컴퓨터 캡처** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="58647-144">The **Capture the Virtual Machine** dialog box appears.</span></span>

8. <span data-ttu-id="58647-145">**이미지 이름**에 새 이미지의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="58647-145">In **Image name**, type a name for the new image.</span></span> <span data-ttu-id="58647-146">**이미지 레이블**에 새 이미지의 레이블을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="58647-146">In **Image label**, type a label for the new image.</span></span>

9. <span data-ttu-id="58647-147">**가상 컴퓨터에서 Sysprep를 실행했습니다**를 클릭하세요.</span><span class="sxs-lookup"><span data-stu-id="58647-147">Click **I've run Sysprep on the virtual machine**.</span></span> <span data-ttu-id="58647-148">이 확인란은 3~5단계에서 Sysprep을 사용하는 작업을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="58647-148">This checkbox refers to the actions with Sysprep in steps 3-5.</span></span> <span data-ttu-id="58647-149">사용자 지정 이미지 집합에 Windows Server 이미지를 추가하기 전에 Sysprep을 실행하여 이미지를 일반화_해야_ 합니다.</span><span class="sxs-lookup"><span data-stu-id="58647-149">An image _must_ be generalized by running Sysprep before you add a Windows Server image to your set of custom images.</span></span>

10. <span data-ttu-id="58647-150">캡처가 완료되면 새 이미지를 **Marketplace** 및 **계산**, **VM 이미지(클래식)** 컨테이너에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58647-150">Once the capture completes, the new image becomes available in the **Marketplace**, in the **Compute**, **VM images (classic)** container.</span></span>

    ![이미지 캡처 성공](./media/capture-image/VMCapturedImageAvailable.png)

## <a name="next-steps"></a><span data-ttu-id="58647-152">다음 단계</span><span class="sxs-lookup"><span data-stu-id="58647-152">Next steps</span></span>
<span data-ttu-id="58647-153">이제 이미지를 사용하여 가상 컴퓨터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58647-153">The image is ready to be used to create virtual machines.</span></span> <span data-ttu-id="58647-154">이를 위해 서비스 메뉴의 아래쪽에 있는 **추가 서비스** 메뉴 항목 및 **계산** 그룹에서 **VM 이미지(클래식)**를 선택하여 가상 컴퓨터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58647-154">To do this, you'll create a virtual machine by selecting the **More services** menu item at the bottom of the services menu, then **VM images (classic)** in the **Compute** group.</span></span> <span data-ttu-id="58647-155">지침에 대해서는 [이미지에서 가상 컴퓨터 만들기](createportal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="58647-155">For instructions, see [Create a virtual machine from an image](createportal.md).</span></span>

[How to sign in to a virtual machine running Windows Server]:connect-logon.md
[How to Use Sysprep: An Introduction]: http://technet.microsoft.com/library/bb457073.aspx
[Run Sysprep.exe]: ./media/virtual-machines-capture-image-windows-server/SysprepCommand.png
[Enter Sysprep.exe options]: ./media/capture-image/SysprepGeneral.png
[The virtual machine is stopped]: ./media/virtual-machines-capture-image-windows-server/SysprepStopped.png
[Capture an image of the virtual machine]: ./media/capture-image/CaptureVM.png
[Enter the image name]: ./media/virtual-machines-capture-image-windows-server/Capture.png
[Image capture successful]: ./media/virtual-machines-capture-image-windows-server/CaptureSuccess.png
[Use the captured image]: ./media/virtual-machines-capture-image-windows-server/MyImagesWindows.png
