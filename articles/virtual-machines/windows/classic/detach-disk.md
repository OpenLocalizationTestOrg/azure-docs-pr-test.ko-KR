---
title: "Windows VM에서 디스크 분리 | Microsoft Docs"
description: "클래식 배포 모델을 사용하는 Azure의 가상 컴퓨터에서 디스크를 분리하는 방법을 알아봅니다."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: b6406768-1726-41bb-9451-1fda0905cc24
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/24/2017
ms.author: cynthn
ms.openlocfilehash: 650c7e10150b95a6ad7cd455746f7c1d77b9b34c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-detach-a-disk-from-a-windows-virtual-machine"></a><span data-ttu-id="b8195-103">Windows 가상 컴퓨터에서 디스크를 분리하는 방법</span><span class="sxs-lookup"><span data-stu-id="b8195-103">How to detach a disk from a Windows virtual machine</span></span>
> [!IMPORTANT]
> <span data-ttu-id="b8195-104">Azure는 리소스를 만들고 작업하기 위한 두 가지 배포 모델로 [Resource Manager와 클래식](../../../resource-manager-deployment-model.md)을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b8195-104">Azure has two distinct deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="b8195-105">이 문서에서는 클래식 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b8195-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="b8195-106">새로운 배포는 대부분 리소스 관리자 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b8195-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="b8195-107">Resource Manager 모델을 사용하는 디스크를 분리하는 방법에 대한 정보는 [여기](../../virtual-machines-windows-detach-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b8195-107">For information about how to detach a disk using the Resource Manager model, see [here](../../virtual-machines-windows-detach-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

[!INCLUDE [howto-detach-disk-windows-linux](../../../../includes/howto-detach-disk-windows-linux.md)]

## <a name="additional-resources"></a><span data-ttu-id="b8195-108">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="b8195-108">Additional resources</span></span>
[<span data-ttu-id="b8195-109">가상 컴퓨터용 디스크 및 VHD에 대하여</span><span class="sxs-lookup"><span data-stu-id="b8195-109">About disks and VHDs for virtual machines</span></span>](../about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[<span data-ttu-id="b8195-110">Windows 가상 컴퓨터에 데이터 디스크를 연결하는 방법</span><span class="sxs-lookup"><span data-stu-id="b8195-110">How to attach a data disk to a Windows virtual machine</span></span>](attach-disk.md)
