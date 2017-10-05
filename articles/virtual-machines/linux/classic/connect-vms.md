---
title: "클라우드 서비스에서 Linux VM 연결 | Microsoft Docs"
description: "클래식 배포 모델을 사용하여 만든 Linux 가상 컴퓨터를 Azure 클라우드 서비스 또는 가상 네트워크에 연결합니다."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 2fd23055-6b34-4ef0-88a8-fc19e32fb3c9
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: cynthn
ms.openlocfilehash: e222645509640b104410f87e4bcd22834c8d9ec1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-linux-virtual-machines-created-with-the-classic-deployment-model-with-a-virtual-network-or-cloud-service"></a><span data-ttu-id="b8005-103">클래식 배포 모델을 사용하여 만든 Linux 가상 컴퓨터를 가상 네트워크 또는 클라우드 서비스에 연결</span><span class="sxs-lookup"><span data-stu-id="b8005-103">Connect Linux virtual machines created with the classic deployment model with a virtual network or cloud service</span></span>
> [!IMPORTANT]
> <span data-ttu-id="b8005-104">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8005-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="b8005-105">이 문서에서는 클래식 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b8005-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="b8005-106">새로운 배포는 대부분 리소스 관리자 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b8005-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="b8005-107">클래식 배포 모델을 사용하여 만든 Linux 가상 컴퓨터는 항상 클라우드 서비스에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8005-107">Linux virtual machines created with the classic deployment model are always placed in a cloud service.</span></span> <span data-ttu-id="b8005-108">클라우드 컴퓨터는 컨테이너 역할을 하며 인터넷을 통해 가상 컴퓨터에 액세스할 수 있도록 고유한 공용 DNS 이름, 공용 IP 주소 및 끝점 집합을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b8005-108">The cloud service acts as a container and provides a unique public DNS name, a public IP address, and a set of endpoints to access the virtual machine over the Internet.</span></span> <span data-ttu-id="b8005-109">클라우드 서비스는 가상 네트워크에 있을 수 있지만 요구 사항은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="b8005-109">The cloud service can be in a virtual network, but that's not a requirement.</span></span> <span data-ttu-id="b8005-110">또한 [Windows 가상 컴퓨터를 가상 네트워크 또는 클라우드 서비스와 연결](../../windows/classic/connect-vms.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8005-110">You can also [connect Windows virtual machines with a virtual network or cloud service](../../windows/classic/connect-vms.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="b8005-111">가상 네트워크에 없는 클라우드 서비스를 *독립 실행형* 클라우드 서비스라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8005-111">If a cloud service isn't in a virtual network, it's called a *standalone* cloud service.</span></span> <span data-ttu-id="b8005-112">독립 실행형 클라우드 서비스의 가상 컴퓨터는 다른 가상 컴퓨터의 공용 DNS 이름을 사용하여 다른 가상 컴퓨터와 통신하고 인터넷을 통해 트래픽을 이동시킵니다.</span><span class="sxs-lookup"><span data-stu-id="b8005-112">The virtual machines in a standalone cloud service communicate with other virtual machines by using the other virtual machines’ public DNS names, and the traffic travels over the Internet.</span></span> <span data-ttu-id="b8005-113">클라우드 서비스가 가상 네트워크에 있는 경우 해당 클라우드 서비스의 가상 컴퓨터는 인터넷을 통해 트래픽을 보내지 않고도 가상 네트워크에 있는 다른 모든 가상 컴퓨터와 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8005-113">If a cloud service is in a virtual network, the virtual machines in that cloud service can communicate with all other virtual machines in the virtual network without sending any traffic over the Internet.</span></span>

<span data-ttu-id="b8005-114">같은 독립 실행형 클라우드 서비스에 가상 컴퓨터를 배치하는 경우에는 계속 부하 분산 및 가용성 집합을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8005-114">If you place your virtual machines in the same standalone cloud service, you can still use load balancing and availability sets.</span></span> <span data-ttu-id="b8005-115">자세한 내용은 [가상 컴퓨터 부하 분산](../../virtual-machines-linux-load-balance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 및 [가상 컴퓨터의 가용성 관리](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b8005-115">For details, see [Load balancing virtual machines](../../virtual-machines-linux-load-balance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) and [Manage the availability of virtual machines](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="b8005-116">그러나 서브넷에서 가상 컴퓨터를 구성하거나 독립 실행형 클라우드 서비스를 온-프레미스 네트워크에 연결할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b8005-116">However, you can't organize the virtual machines on subnets or connect a standalone cloud service to your on-premises network.</span></span> <span data-ttu-id="b8005-117">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b8005-117">Here's an example:</span></span>

[!INCLUDE [virtual-machines-common-classic-connect-vms](../../../../includes/virtual-machines-common-classic-connect-vms.md)]

## <a name="next-steps"></a><span data-ttu-id="b8005-118">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b8005-118">Next steps</span></span>
<span data-ttu-id="b8005-119">가상 컴퓨터를 만들고 나서 서비스 및 워크로드에 데이터를 저장할 위치가 포함되도록 [데이터 디스크를 추가](attach-disk.md) 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b8005-119">After you create a virtual machine, it's a good idea to [add a data disk](attach-disk.md) so your services and workloads have a location to store data.</span></span>
