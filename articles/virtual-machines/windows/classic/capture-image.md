---
title: "Windows Azure VM의 이미지 aaaCapture | Microsoft Docs"
description: "Hello 클래식 배포 모델을 사용 하 여 만든 Azure Windows 가상 컴퓨터의 이미지를 캡처하십시오."
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
ms.openlocfilehash: b9bbc437012aa44295f90941c9d72e39509df28f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="capture-an-image-of-an-azure-windows-virtual-machine-created-with-hello-classic-deployment-model"></a><span data-ttu-id="739cd-103">Hello 클래식 배포 모델을 사용 하 여 만든 Azure Windows 가상 컴퓨터의 이미지를 캡처하십시오.</span><span class="sxs-lookup"><span data-stu-id="739cd-103">Capture an image of an Azure Windows virtual machine created with hello classic deployment model.</span></span>
> [!IMPORTANT]
> <span data-ttu-id="739cd-104">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="739cd-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="739cd-105">이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="739cd-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="739cd-106">대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="739cd-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="739cd-107">Resource Manager 모델 정보는 [Azure에서 일반화된 VM의 관리되는 이미지 캡처](../capture-image-resource.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="739cd-107">For Resource Manager model information, see [Capture a managed image of a generalized VM in Azure](../capture-image-resource.md).</span></span>

<span data-ttu-id="739cd-108">이 문서에서는 어떻게 toocapture Windows 이미지 toocreate로 사용할 수 있도록 다른 가상 컴퓨터를 실행 하는 Azure 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="739cd-108">This article shows you how toocapture an Azure virtual machine running Windows so you can use it as an image toocreate other virtual machines.</span></span> <span data-ttu-id="739cd-109">이 이미지에 hello 운영 체제 디스크는 및 모든 데이터 디스크에 toohello 가상 컴퓨터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="739cd-109">This image includes hello operating system disk and any data disks that are attached toohello virtual machine.</span></span> <span data-ttu-id="739cd-110">네트워킹 구성, 까다롭기 때문에 네트워크 구성을 tooset hello hello 이미지를 사용 하는 다른 가상 컴퓨터를 만들 때 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="739cd-110">It doesn't include networking configurations, so you'll need tooset up network configurations when you create hello other virtual machines that use hello image.</span></span>

<span data-ttu-id="739cd-111">Azure 저장소에서 이미지 hello **VM 이미지 (클래식)**, **계산** 모두를 볼 때 나열 되 서비스에 hello Azure 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="739cd-111">Azure stores hello image under **VM images (classic)**, a **Compute** service that is listed when you view all hello Azure services.</span></span> <span data-ttu-id="739cd-112">이 hello 업로드 한 이미지가 저장 된 같은 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="739cd-112">This is hello same place where any images you've uploaded are stored.</span></span> <span data-ttu-id="739cd-113">이미지에 대한 자세한 내용은 [가상 컴퓨터 이미지 정보](about-images.md?toc=%2fazure%2fvirtual-machines%2fWindows%2fclassic%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="739cd-113">For details about images, see [About images for virtual machines](about-images.md?toc=%2fazure%2fvirtual-machines%2fWindows%2fclassic%2ftoc.json).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="739cd-114">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="739cd-114">Before you begin</span></span>
<span data-ttu-id="739cd-115">이러한 단계는 이미 Azure 가상 컴퓨터 생성 되었으며 모든 데이터 디스크를 연결까지 포함 하는 hello 운영 체제 구성 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="739cd-115">These steps assume that you've already created an Azure virtual machine and configured hello operating system, including attaching any data disks.</span></span> <span data-ttu-id="739cd-116">아직이 hello 내용은 문서 작성 및 hello 가상 컴퓨터 준비 중에 다음을 참조.</span><span class="sxs-lookup"><span data-stu-id="739cd-116">If you haven't done this yet, see hello following articles for information on creating and preparing hello virtual machine:</span></span>

* [<span data-ttu-id="739cd-117">이미지에서 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="739cd-117">Create a virtual machine from an image</span></span>](createportal.md)
* [<span data-ttu-id="739cd-118">어떻게 tooattach 데이터 디스크 tooa 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="739cd-118">How tooattach a data disk tooa virtual machine</span></span>](attach-disk.md)
* <span data-ttu-id="739cd-119">Hello 서버 역할 Sysprep로 사용할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="739cd-119">Make sure hello server roles are supported with Sysprep.</span></span> <span data-ttu-id="739cd-120">자세한 내용은 [서버 역할에 대한 Sysprep 지원](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="739cd-120">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span></span>

> [!WARNING]
> <span data-ttu-id="739cd-121">이 프로세스는 캡처된 후 hello 원래 가상 컴퓨터를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="739cd-121">This process deletes hello original virtual machine after it's captured.</span></span>
>
>

<span data-ttu-id="739cd-122">권장 되는 Azure 가상 컴퓨터의 이미지 이전 toocapturing hello 대상 가상 컴퓨터를 백업 합니다.</span><span class="sxs-lookup"><span data-stu-id="739cd-122">Prior toocapturing an image of an Azure virtual machine, it is recommended hello target virtual machine be backed up.</span></span> <span data-ttu-id="739cd-123">Azure 백업을 사용하여 Azure 가상 컴퓨터를 백업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="739cd-123">Azure virtual machines can be backed up using Azure Backup.</span></span> <span data-ttu-id="739cd-124">자세한 내용은 [Azure 가상 컴퓨터 백업](../../../backup/backup-azure-vms.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="739cd-124">For details, see [Back up Azure virtual machines](../../../backup/backup-azure-vms.md).</span></span> <span data-ttu-id="739cd-125">다른 솔루션은 인증된 파트너에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="739cd-125">Other solutions are available from certified partners.</span></span> <span data-ttu-id="739cd-126">현재 사용할 수 있는 항목을 toofind hello Azure 마켓플레이스를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="739cd-126">toofind out what’s currently available, search hello Azure Marketplace.</span></span>

## <a name="capture-hello-virtual-machine"></a><span data-ttu-id="739cd-127">Hello 가상 컴퓨터 캡처</span><span class="sxs-lookup"><span data-stu-id="739cd-127">Capture hello virtual machine</span></span>
1. <span data-ttu-id="739cd-128">Hello에 [Azure 포털](http://portal.azure.com), **연결** toohello 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="739cd-128">In hello [Azure portal](http://portal.azure.com), **Connect** toohello virtual machine.</span></span> <span data-ttu-id="739cd-129">자세한 내용은 [어떻게 toosign Windows Server를 실행 하는 tooa 가상 컴퓨터에서][How toosign in tooa virtual machine running Windows Server]합니다.</span><span class="sxs-lookup"><span data-stu-id="739cd-129">For instructions, see [How toosign in tooa virtual machine running Windows Server][How toosign in tooa virtual machine running Windows Server].</span></span>
2. <span data-ttu-id="739cd-130">관리자로 명령 프롬프트 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="739cd-130">Open a Command Prompt window as an administrator.</span></span>
3. <span data-ttu-id="739cd-131">Hello 디렉터리도 변경`%windir%\system32\sysprep`, 한 다음 sysprep.exe를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="739cd-131">Change hello directory too`%windir%\system32\sysprep`, and then run sysprep.exe.</span></span>
4. <span data-ttu-id="739cd-132">hello **시스템 준비 도구** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="739cd-132">hello **System Preparation Tool** dialog box appears.</span></span> <span data-ttu-id="739cd-133">다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="739cd-133">Do hello following:</span></span>

   * <span data-ttu-id="739cd-134">**시스템 정리 작업**에서 **시스템 OOBE(첫 실행 경험) 입력**을 선택하고 **일반화**를 선택했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="739cd-134">In **System Cleanup Action**, select **Enter System Out-of-Box Experience (OOBE)** and make sure that **Generalize** is checked.</span></span> <span data-ttu-id="739cd-135">Sysprep를 사용 하는 방법에 대 한 자세한 내용은 참조 [어떻게 tooUse Sysprep: 소개][How tooUse Sysprep: An Introduction]합니다.</span><span class="sxs-lookup"><span data-stu-id="739cd-135">For more information about using Sysprep, see [How tooUse Sysprep: An Introduction][How tooUse Sysprep: An Introduction].</span></span>
   * <span data-ttu-id="739cd-136">**종료 옵션**에서 **종료**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="739cd-136">In **Shutdown Options**, select **Shutdown**.</span></span>
   * <span data-ttu-id="739cd-137">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="739cd-137">Click **OK**.</span></span>

   ![Sysprep 실행](./media/capture-image/SysprepGeneral.png)
5. <span data-ttu-id="739cd-139">Sysprep 쪽 hello Azure 포털에서에서 가상 컴퓨터 hello의 hello 상태를 변경 하는 hello 가상 컴퓨터 종료**Stopped**합니다.</span><span class="sxs-lookup"><span data-stu-id="739cd-139">Sysprep shuts down hello virtual machine, which changes hello status of hello virtual machine in hello Azure portal too**Stopped**.</span></span>
6. <span data-ttu-id="739cd-140">Hello Azure 포털에서에서 클릭 **가상 컴퓨터 (클래식)** 선택 hello toocapture 가상 컴퓨터 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="739cd-140">In hello Azure portal, click **Virtual Machines (classic)** and select hello virtual machine you want toocapture.</span></span> <span data-ttu-id="739cd-141">hello **VM 이미지 (클래식)** 그룹 아래에 있는지 **계산** 볼 때 **더 많은 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="739cd-141">hello **VM images (classic)** group is listed under **Compute** when you view **More services**.</span></span>

7. <span data-ttu-id="739cd-142">Hello 명령 모음에서 **캡처**합니다.</span><span class="sxs-lookup"><span data-stu-id="739cd-142">On hello command bar, click **Capture**.</span></span>

   ![가상 컴퓨터 캡처](./media/capture-image/CaptureVM.png)

   <span data-ttu-id="739cd-144">hello **가상 컴퓨터 캡처 hello** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="739cd-144">hello **Capture hello Virtual Machine** dialog box appears.</span></span>

8. <span data-ttu-id="739cd-145">**이미지 이름**를 hello 새 이미지의 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="739cd-145">In **Image name**, type a name for hello new image.</span></span> <span data-ttu-id="739cd-146">**이미지 레이블**를 hello 새 이미지에 대 한 레이블을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="739cd-146">In **Image label**, type a label for hello new image.</span></span>

9. <span data-ttu-id="739cd-147">클릭 **hello 가상 컴퓨터에서 Sysprep을 실행 했습니다**합니다.</span><span class="sxs-lookup"><span data-stu-id="739cd-147">Click **I've run Sysprep on hello virtual machine**.</span></span> <span data-ttu-id="739cd-148">이 확인란을 3-5 단계에서 Sysprep 사용 하 여 toohello 동작을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="739cd-148">This checkbox refers toohello actions with Sysprep in steps 3-5.</span></span> <span data-ttu-id="739cd-149">이미지 _해야_ Sysprep을 실행 하는 Windows 서버를 추가 하기 전에 이미지 tooyour 집합이 사용자 지정 이미지를 일반화 합니다.</span><span class="sxs-lookup"><span data-stu-id="739cd-149">An image _must_ be generalized by running Sysprep before you add a Windows Server image tooyour set of custom images.</span></span>

10. <span data-ttu-id="739cd-150">Hello 캡처 완료 되 면 hello 새 이미지에서에서 사용할 수 있게 hello **마켓플레이스**, hello에 **계산**, **VM 이미지 (클래식)** 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="739cd-150">Once hello capture completes, hello new image becomes available in hello **Marketplace**, in hello **Compute**, **VM images (classic)** container.</span></span>

    ![이미지 캡처 성공](./media/capture-image/VMCapturedImageAvailable.png)

## <a name="next-steps"></a><span data-ttu-id="739cd-152">다음 단계</span><span class="sxs-lookup"><span data-stu-id="739cd-152">Next steps</span></span>
<span data-ttu-id="739cd-153">hello 이미지는 사용 되는 준비 toobe toocreate 가상 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="739cd-153">hello image is ready toobe used toocreate virtual machines.</span></span> <span data-ttu-id="739cd-154">toodo이 hello를 선택 하 여 가상 컴퓨터를 만들어 **더 많은 서비스** hello 서비스 메뉴에서 다음의 hello 맨 아래에 있는 메뉴 항목 **VM 이미지 (클래식)** hello에 **계산**그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="739cd-154">toodo this, you'll create a virtual machine by selecting hello **More services** menu item at hello bottom of hello services menu, then **VM images (classic)** in hello **Compute** group.</span></span> <span data-ttu-id="739cd-155">지침에 대해서는 [이미지에서 가상 컴퓨터 만들기](createportal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="739cd-155">For instructions, see [Create a virtual machine from an image](createportal.md).</span></span>

[How toosign in tooa virtual machine running Windows Server]:connect-logon.md
[How tooUse Sysprep: An Introduction]: http://technet.microsoft.com/library/bb457073.aspx
[Run Sysprep.exe]: ./media/virtual-machines-capture-image-windows-server/SysprepCommand.png
[Enter Sysprep.exe options]: ./media/capture-image/SysprepGeneral.png
[hello virtual machine is stopped]: ./media/virtual-machines-capture-image-windows-server/SysprepStopped.png
[Capture an image of hello virtual machine]: ./media/capture-image/CaptureVM.png
[Enter hello image name]: ./media/virtual-machines-capture-image-windows-server/Capture.png
[Image capture successful]: ./media/virtual-machines-capture-image-windows-server/CaptureSuccess.png
[Use hello captured image]: ./media/virtual-machines-capture-image-windows-server/MyImagesWindows.png
