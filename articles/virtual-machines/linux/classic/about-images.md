---
title: "Azure의 Linux VM 이미지 정보 | Microsoft Docs"
description: "Azure의 가상 컴퓨터에서 Linux 이미지를 사용하는 방법에 대해 알아봅니다."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: e6ea8adc-4e7a-467a-9394-cd05e67898b7
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/21/2016
ms.author: cynthn
ms.openlocfilehash: 187642db18806f4034dcecf4c25b5c71028fdfe3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="about-images-for-linux-virtual-machines"></a><span data-ttu-id="350c3-103">Linux 가상 컴퓨터에 대한 이미지 정보</span><span class="sxs-lookup"><span data-stu-id="350c3-103">About images for Linux virtual machines</span></span>
> [!IMPORTANT]
> <span data-ttu-id="350c3-104">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="350c3-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="350c3-105">이 문서에서는 클래식 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="350c3-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="350c3-106">새로운 배포는 대부분 리소스 관리자 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="350c3-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="350c3-107">Resource Manager 모델을 사용하는 이미지에 대한 정보는 [여기](../cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="350c3-107">For information about images using the Resource Manager model, see [here](../cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-classic-about-images](../../../../includes/virtual-machines-common-classic-about-images.md)]

## <a name="working-with-images"></a><span data-ttu-id="350c3-108">이미지 작업</span><span class="sxs-lookup"><span data-stu-id="350c3-108">Working with images</span></span>
<span data-ttu-id="350c3-109">Azure 구독에 사용할 수 있는 이미지를 관리하려면 Mac, Linux 및 Windows용에 대한 Azure CLI(명령줄 인터페이스)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="350c3-109">You can use the Azure Command-Line Interface (CLI) for Mac, Linux, and Windows to manage the images available to your Azure subscription.</span></span> <span data-ttu-id="350c3-110">또한 일부 이미지 작업에 Azure 포털을 사용할 수 있지만 명령줄에는 추가 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="350c3-110">You also can use the Azure portal for some image tasks, but the command line gives you more options.</span></span>

<span data-ttu-id="350c3-111">도구 사용 예제를 보려면 [Linux 및 Mac의 일반적 Azure CLI 명령](../cli-manage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="350c3-111">For examples of using the tools, see [Common Azure CLI commands on Linux and Mac](../cli-manage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="350c3-112">다음 단계</span><span class="sxs-lookup"><span data-stu-id="350c3-112">Next steps</span></span>
<span data-ttu-id="350c3-113">[사용자 고유의 이미지를 업로드](create-upload-vhd.md)할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="350c3-113">You can also [upload your own image](create-upload-vhd.md).</span></span>
