---
title: "Azure Portal에서 VM 만들기 | Microsoft Docs"
description: "Azure 포털에서 Windows 가상 컴퓨터만들기"
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
ms.openlocfilehash: 0981872ff819fdf49a9cc97afce3c212013ce76b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-virtual-machine-running-windows-in-the-azure-portal"></a><span data-ttu-id="ea6cd-103">Azure 포털에서 Windows를 실행하는 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="ea6cd-103">Create a virtual machine running Windows in the Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ea6cd-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="ea6cd-104">Azure portal</span></span>](tutorial.md)
> * [<span data-ttu-id="ea6cd-105">PowerShell: 클래식 배포</span><span class="sxs-lookup"><span data-stu-id="ea6cd-105">PowerShell: Classic deployment</span></span>](create-powershell.md)
>
>

<br>

> [!IMPORTANT]
> <span data-ttu-id="ea6cd-106">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea6cd-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="ea6cd-107">이 문서에서는 클래식 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="ea6cd-107">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="ea6cd-108">새로운 배포는 대부분 리소스 관리자 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ea6cd-108">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="ea6cd-109">**Azure Portal**을 통해 [Resource Manager 배포 모델을 사용하여 이러한 단계를 수행하는 방법](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ea6cd-109">Learn how to [perform these steps using the Resource Manager deployment model](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) using the **Azure portal**.</span></span>

<span data-ttu-id="ea6cd-110">이 자습서에서는 Azure Portal에서 Windows를 실행하는 Azure VM(가상 컴퓨터)을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ea6cd-110">This tutorial shows you how to create an Azure virtual machine (VM) running Windows in the Azure portal.</span></span> <span data-ttu-id="ea6cd-111">한 예로, Windows Server 이미지를 사용할 것이지만, 해당 아미지는 Azure가 제공하는 여러 이미지 중 하나일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="ea6cd-111">We'll use a Windows Server image as an example, but that's just one of the many images Azure offers.</span></span> <span data-ttu-id="ea6cd-112">참고: 이미지 선택은 구독에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="ea6cd-112">Note that your image choices depend on your subscription.</span></span> <span data-ttu-id="ea6cd-113">예를 들어 Windows 데스크톱 이미지는 MSDN 구독자가 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea6cd-113">For example, Windows desktop images may be available to MSDN subscribers.</span></span>

<span data-ttu-id="ea6cd-114">이 섹션에서는 Azure Portal에서 **대시보드**를 사용하여 가상 컴퓨터를 선택하고 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ea6cd-114">This section shows you how to use the **Dashboard** in the Azure portal to select and then create the virtual machine.</span></span>

<span data-ttu-id="ea6cd-115">[사용자 고유의 이미지](createupload-vhd.md)를 사용하여 VM을 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea6cd-115">You can also create VMs using [your own images](createupload-vhd.md).</span></span> <span data-ttu-id="ea6cd-116">이 방법 및 다른 방법에 대한 자세한 내용은 [Windows 가상 컴퓨터를 만드는 다양한 방법](../../virtual-machines-windows-creation-choices.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ea6cd-116">To learn about this and other methods, see [Different ways to create a Windows virtual machine](../../virtual-machines-windows-creation-choices.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<!-- 02/27/2017 Video removed as it was based on the classic portal. -->

## <span data-ttu-id="ea6cd-117"><a id="createvirtualmachine"> </a>가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="ea6cd-117"><a id="createvirtualmachine"> </a>Create the virtual machine</span></span>
[!INCLUDE [virtual-machines-create-WindowsVM](../../../../includes/virtual-machines-create-windowsvm.md)]

## <a name="next-steps"></a><span data-ttu-id="ea6cd-118">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ea6cd-118">Next steps</span></span>
* <span data-ttu-id="ea6cd-119">Azure Portal에서 [Resource Manager 배포 모델을 사용하여 VM을 만드는 방법](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ea6cd-119">Learn how to [create a VM using the Resource Manager deployment model](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) in the Azure portal.</span></span>
* <span data-ttu-id="ea6cd-120">가상 컴퓨터에 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="ea6cd-120">Log on to the virtual machine.</span></span> <span data-ttu-id="ea6cd-121">지침은 [Windows Server를 실행하는 가상 컴퓨터에 로그온](connect-logon.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ea6cd-121">For instructions, see [Log on to a virtual machine running Windows Server](connect-logon.md).</span></span>
* <span data-ttu-id="ea6cd-122">데이터를 저장할 디스크를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="ea6cd-122">Attach a disk to store data.</span></span> <span data-ttu-id="ea6cd-123">빈 디스크와 데이터가 포함된 디스크를 모두 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea6cd-123">You can attach both empty disks and disks that contain data.</span></span> <span data-ttu-id="ea6cd-124">지침은 [클래식 배포 모델을 사용하여 만든 Windows 가상 컴퓨터에 데이터 디스크 연결](attach-disk.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ea6cd-124">For instructions, see the [Attach a data disk to a Windows virtual machine created with the classic deployment model](attach-disk.md).</span></span>
