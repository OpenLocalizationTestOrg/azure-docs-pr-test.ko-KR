---
title: "hello Azure 포털에서에서 VM aaaCreate | Microsoft Docs"
description: "Hello Azure 포털에서에서 Windows 가상 컴퓨터를 만듭니다."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1871f823-ebd7-4eff-9a22-8e2411555595
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: 3848a3d06a7ce377633db78ea385826ed40f94fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-running-windows-in-hello-azure-portal"></a><span data-ttu-id="59613-103">Hello Azure 포털에서에서 Windows를 실행 하는 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="59613-103">Create a virtual machine running Windows in hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="59613-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="59613-104">Azure portal</span></span>](tutorial.md)
> * [<span data-ttu-id="59613-105">PowerShell: 클래식 배포</span><span class="sxs-lookup"><span data-stu-id="59613-105">PowerShell: Classic deployment</span></span>](create-powershell.md)
>
>

<br>

> [!IMPORTANT]
> <span data-ttu-id="59613-106">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59613-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="59613-107">이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="59613-107">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="59613-108">대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="59613-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="59613-109">너무 방법에 대해 알아봅니다[hello 리소스 관리자 배포 모델을 사용 하 여 이러한 단계를 수행](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) hello를 사용 하 여 **Azure 포털**합니다.</span><span class="sxs-lookup"><span data-stu-id="59613-109">Learn how too[perform these steps using hello Resource Manager deployment model](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) using hello **Azure portal**.</span></span>

<span data-ttu-id="59613-110">이 자습서에서는 어떻게 toocreate Azure 가상 컴퓨터 (VM) hello Azure 포털에서에서 Windows를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="59613-110">This tutorial shows you how toocreate an Azure virtual machine (VM) running Windows in hello Azure portal.</span></span> <span data-ttu-id="59613-111">예를 들어, Windows Server 이미지에서는 하지만 하는 것 외의 hello 여러 Azure 제안의 이미지입니다.</span><span class="sxs-lookup"><span data-stu-id="59613-111">We'll use a Windows Server image as an example, but that's just one of hello many images Azure offers.</span></span> <span data-ttu-id="59613-112">참고: 이미지 선택은 구독에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="59613-112">Note that your image choices depend on your subscription.</span></span> <span data-ttu-id="59613-113">예를 들어 Windows 데스크톱 이미지는 사용 가능한 tooMSDN 구독자 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59613-113">For example, Windows desktop images may be available tooMSDN subscribers.</span></span>

<span data-ttu-id="59613-114">이 섹션에서는 toouse hello **대시보드** Azure 포털 tooselect hello와 다음 hello 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="59613-114">This section shows you how toouse hello **Dashboard** in hello Azure portal tooselect and then create hello virtual machine.</span></span>

<span data-ttu-id="59613-115">[사용자 고유의 이미지](createupload-vhd.md)를 사용하여 VM을 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59613-115">You can also create VMs using [your own images](createupload-vhd.md).</span></span> <span data-ttu-id="59613-116">toolearn이 및 다른 방법에 대 한 참조 [Windows 가상 컴퓨터를 다른 방법으로 toocreate](../../virtual-machines-windows-creation-choices.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="59613-116">toolearn about this and other methods, see [Different ways toocreate a Windows virtual machine](../../virtual-machines-windows-creation-choices.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<!-- 02/27/2017 Video removed as it was based on hello classic portal. -->

## <span data-ttu-id="59613-117"><a id="createvirtualmachine"></a>Hello 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="59613-117"><a id="createvirtualmachine"> </a>Create hello virtual machine</span></span>
[!INCLUDE [virtual-machines-create-WindowsVM](../../../../includes/virtual-machines-create-windowsvm.md)]

## <a name="next-steps"></a><span data-ttu-id="59613-118">다음 단계</span><span class="sxs-lookup"><span data-stu-id="59613-118">Next steps</span></span>
* <span data-ttu-id="59613-119">너무 방법에 대해 알아봅니다[hello 리소스 관리자 배포 모델을 사용 하 여 VM 만들기](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) hello Azure 포털의에서.</span><span class="sxs-lookup"><span data-stu-id="59613-119">Learn how too[create a VM using hello Resource Manager deployment model](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) in hello Azure portal.</span></span>
* <span data-ttu-id="59613-120">Toohello 가상 컴퓨터에 로그온 합니다.</span><span class="sxs-lookup"><span data-stu-id="59613-120">Log on toohello virtual machine.</span></span> <span data-ttu-id="59613-121">자세한 내용은 [Windows Server를 실행 하는 tooa 가상 컴퓨터에 로그온](connect-logon.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="59613-121">For instructions, see [Log on tooa virtual machine running Windows Server](connect-logon.md).</span></span>
* <span data-ttu-id="59613-122">디스크 toostore 데이터에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="59613-122">Attach a disk toostore data.</span></span> <span data-ttu-id="59613-123">빈 디스크와 데이터가 포함된 디스크를 모두 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="59613-123">You can attach both empty disks and disks that contain data.</span></span> <span data-ttu-id="59613-124">자세한 내용은 hello [hello 클래식 배포 모델을 사용 하 여 만든 데이터 디스크 tooa Windows 가상 컴퓨터를 연결](attach-disk.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="59613-124">For instructions, see hello [Attach a data disk tooa Windows virtual machine created with hello classic deployment model](attach-disk.md).</span></span>
