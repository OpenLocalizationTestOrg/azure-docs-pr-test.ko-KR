---
title: "클래식 Linux VM에 끝점을 aaaSet | Microsoft Docs"
description: "Azure에서 Linux 가상 컴퓨터를 사용 하 여 hello Azure 클래식 포털 tooallow 통신에서에서 Linux VM에 대 한 끝점을 tooset에 알아봅니다"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: f3749738-1109-4a1d-8635-40e4bd220e91
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: cynthn
ms.openlocfilehash: 1c959d10dd1e20228fa4a20e1cc0205c1d12f185
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-up-endpoints-on-a-linux-classic-virtual-machine-in-azure"></a><span data-ttu-id="7a384-103">어떻게 tooset Azure에서 Linux 클래식 가상 컴퓨터에 끝점을</span><span class="sxs-lookup"><span data-stu-id="7a384-103">How tooset up endpoints on a Linux classic virtual machine in Azure</span></span>
<span data-ttu-id="7a384-104">Hello에 다른 가상 컴퓨터와 개인 네트워크 채널을 통해 hello 클래식 배포 모델을 사용 하 여 Azure에서 만드는 모든 Linux 가상 컴퓨터 자동으로 통신할 수 있습니다이 동일한 클라우드 서비스 또는 가상 네트워크.</span><span class="sxs-lookup"><span data-stu-id="7a384-104">All Linux virtual machines that you create in Azure using hello classic deployment model can automatically communicate over a private network channel with other virtual machines in hello same cloud service or virtual network.</span></span> <span data-ttu-id="7a384-105">그러나 hello 인터넷 또는 다른 가상 네트워크에 있는 컴퓨터에 끝점 toodirect hello 인바운드 네트워크 트래픽을 tooa 가상 컴퓨터가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7a384-105">However, computers on hello Internet or other virtual networks require endpoints toodirect hello inbound network traffic tooa virtual machine.</span></span> <span data-ttu-id="7a384-106">이 문서는 [Windows 가상 컴퓨터](../../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)에도 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a384-106">This article is also available for [Windows virtual machines](../../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7a384-107">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a384-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="7a384-108">이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a384-108">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="7a384-109">대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7a384-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="7a384-110">Hello에 **리소스 관리자** 배포 모델을 사용 하 여 끝점이 구성 **(Nsg) 네트워크 보안 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="7a384-110">In hello **Resource Manager** deployment model, endpoints are configured using **Network Security Groups (NSGs)**.</span></span> <span data-ttu-id="7a384-111">자세한 내용은 [포트 및 끝점 열기](../nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7a384-111">For more information, see [Opening ports and endpoints](../nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="7a384-112">Hello Azure 포털에서에서 Linux 가상 컴퓨터를 만들 때 끝점에 대 한 SSH (보안 셸) 일반적으로 사용자에 대 한 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="7a384-112">When you create a Linux virtual machine in hello Azure portal, an endpoint for Secure Shell (SSH) is typically created for you automatically.</span></span> <span data-ttu-id="7a384-113">Hello 가상 컴퓨터를 만드는 동안 또는 나중에 필요에 따라 추가 끝점을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a384-113">You can configure additional endpoints while creating hello virtual machine or afterwards as needed.</span></span>

[!INCLUDE [virtual-machines-common-classic-setup-endpoints](../../../../includes/virtual-machines-common-classic-setup-endpoints.md)]

## <a name="next-steps"></a><span data-ttu-id="7a384-114">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7a384-114">Next steps</span></span>
* <span data-ttu-id="7a384-115">Hello를 사용 하 여 VM 끝점을 만들 수도 있습니다 [Azure 명령줄 인터페이스](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)합니다.</span><span class="sxs-lookup"><span data-stu-id="7a384-115">You can also create a VM endpoint by using hello [Azure Command-Line Interface](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span> <span data-ttu-id="7a384-116">Hello 실행 **azure vm 끝점 만들기** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="7a384-116">Run hello **azure vm endpoint create** command.</span></span>
* <span data-ttu-id="7a384-117">Hello 리소스 관리자 배포 모델에서 가상 컴퓨터를 만든 경우 리소스 관리자 모드에서 Azure CLI hello을도 사용할 수 있습니다[네트워크 보안 그룹을 만들고](../../../virtual-network/virtual-networks-create-nsg-arm-cli.md) toocontrol 트래픽 toohello VM입니다.</span><span class="sxs-lookup"><span data-stu-id="7a384-117">If you created a virtual machine in hello Resource Manager deployment model, you can use hello Azure CLI in Resource Manager mode too[create network security groups](../../../virtual-network/virtual-networks-create-nsg-arm-cli.md) toocontrol traffic toohello VM.</span></span>
