---
title: "클래식 Linux VM에서 끝점 설정 | Microsoft Docs"
description: "Azure에서 Linux 가상 컴퓨터와 통신을 허용하도록 Azure 클래식 포털에서 Linux VM에 대한 끝점을 설정하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 4fd8b847b0f60648d1661ce5a8667c641e616ed4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-set-up-endpoints-on-a-linux-classic-virtual-machine-in-azure"></a><span data-ttu-id="2502f-103">Azure에서 Linux 클래식 가상 컴퓨터에 끝점을 설정하는 방법</span><span class="sxs-lookup"><span data-stu-id="2502f-103">How to set up endpoints on a Linux classic virtual machine in Azure</span></span>
<span data-ttu-id="2502f-104">클래식 배포 모델을 사용하여 Azure에서 만든 모든 Linux 가상 컴퓨터는 개인 네트워크 채널을 통해 동일한 클라우드 서비스 또는 가상 네트워크에 있는 다른 가상 컴퓨터와 자동으로 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2502f-104">All Linux virtual machines that you create in Azure using the classic deployment model can automatically communicate over a private network channel with other virtual machines in the same cloud service or virtual network.</span></span> <span data-ttu-id="2502f-105">그러나 인터넷이나 다른 가상 네트워크의 컴퓨터가 가상 컴퓨터로 인바운드 네트워크 트래픽을 전달하려면 끝점이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2502f-105">However, computers on the Internet or other virtual networks require endpoints to direct the inbound network traffic to a virtual machine.</span></span> <span data-ttu-id="2502f-106">이 문서는 [Windows 가상 컴퓨터](../../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)에도 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2502f-106">This article is also available for [Windows virtual machines](../../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2502f-107">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2502f-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="2502f-108">이 문서에서는 클래식 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="2502f-108">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="2502f-109">새로운 배포는 대부분 리소스 관리자 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2502f-109">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="2502f-110">**Resource Manager** 배포 모델에서는 **NSG(네트워크 보안 그룹)**를 사용하여 끝점을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="2502f-110">In the **Resource Manager** deployment model, endpoints are configured using **Network Security Groups (NSGs)**.</span></span> <span data-ttu-id="2502f-111">자세한 내용은 [포트 및 끝점 열기](../nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2502f-111">For more information, see [Opening ports and endpoints](../nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="2502f-112">Azure Portal에서 Linux 가상 컴퓨터를 만들 때 SSH(Secure Shell)에 대한 끝점이 보통 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="2502f-112">When you create a Linux virtual machine in the Azure portal, an endpoint for Secure Shell (SSH) is typically created for you automatically.</span></span> <span data-ttu-id="2502f-113">가상 컴퓨터를 만드는 동안 또는 가상 컴퓨터를 만든 후 필요에 따라 추가 끝점을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2502f-113">You can configure additional endpoints while creating the virtual machine or afterwards as needed.</span></span>

[!INCLUDE [virtual-machines-common-classic-setup-endpoints](../../../../includes/virtual-machines-common-classic-setup-endpoints.md)]

## <a name="next-steps"></a><span data-ttu-id="2502f-114">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2502f-114">Next steps</span></span>
* <span data-ttu-id="2502f-115">[Azure 명령줄 인터페이스](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)를 사용하여 VM 끝점을 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2502f-115">You can also create a VM endpoint by using the [Azure Command-Line Interface](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span> <span data-ttu-id="2502f-116">**azure vm endpoint create** 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2502f-116">Run the **azure vm endpoint create** command.</span></span>
* <span data-ttu-id="2502f-117">리소스 관리자 배포 모델에서 가상 컴퓨터를 만들면, 리소스 관리자에서 Azure CLI를 사용하여 VM에 대한 트래픽을 제어하는 [네트워크 보안 그룹을 만들 수 있습니다](../../../virtual-network/virtual-networks-create-nsg-arm-cli.md) .</span><span class="sxs-lookup"><span data-stu-id="2502f-117">If you created a virtual machine in the Resource Manager deployment model, you can use the Azure CLI in Resource Manager mode to [create network security groups](../../../virtual-network/virtual-networks-create-nsg-arm-cli.md) to control traffic to the VM.</span></span>
