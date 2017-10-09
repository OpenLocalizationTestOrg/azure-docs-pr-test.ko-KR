---
title: "Linux Vm 클라우드 서비스에서 aaaConnect | Microsoft Docs"
description: "Hello 클래식 배포 모델 tooan Azure 클라우드 서비스 또는 가상 네트워크를 사용 하 여 만든 Linux 가상 컴퓨터를 연결 합니다."
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
ms.openlocfilehash: 323baf04390d53ffb2810e24a24d175c08e60cd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-linux-virtual-machines-created-with-hello-classic-deployment-model-with-a-virtual-network-or-cloud-service"></a><span data-ttu-id="97f8e-103">가상 네트워크 또는 클라우드 서비스와 hello 클래식 배포 모델을 사용 하 여 만든 Linux 가상 컴퓨터 연결</span><span class="sxs-lookup"><span data-stu-id="97f8e-103">Connect Linux virtual machines created with hello classic deployment model with a virtual network or cloud service</span></span>
> [!IMPORTANT]
> <span data-ttu-id="97f8e-104">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97f8e-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="97f8e-105">이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f8e-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="97f8e-106">대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="97f8e-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="97f8e-107">Hello 클래식 배포 모델을 사용 하 여 만든 Linux 가상 컴퓨터는 항상 클라우드 서비스에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="97f8e-107">Linux virtual machines created with hello classic deployment model are always placed in a cloud service.</span></span> <span data-ttu-id="97f8e-108">hello 클라우드 서비스 컨테이너 역할을 하 고 hello 인터넷을 통해 고유한 공용 DNS 이름, 공용 IP 주소 및 끝점 tooaccess hello 가상 컴퓨터의 집합을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f8e-108">hello cloud service acts as a container and provides a unique public DNS name, a public IP address, and a set of endpoints tooaccess hello virtual machine over hello Internet.</span></span> <span data-ttu-id="97f8e-109">hello 클라우드 서비스가 가상 네트워크 수 있지만 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="97f8e-109">hello cloud service can be in a virtual network, but that's not a requirement.</span></span> <span data-ttu-id="97f8e-110">또한 [Windows 가상 컴퓨터를 가상 네트워크 또는 클라우드 서비스와 연결](../../windows/classic/connect-vms.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97f8e-110">You can also [connect Windows virtual machines with a virtual network or cloud service](../../windows/classic/connect-vms.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="97f8e-111">가상 네트워크에 없는 클라우드 서비스를 *독립 실행형* 클라우드 서비스라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f8e-111">If a cloud service isn't in a virtual network, it's called a *standalone* cloud service.</span></span> <span data-ttu-id="97f8e-112">hello 가상 컴퓨터가 독립 실행형 클라우드 서비스에 통신할 다른 가상 컴퓨터를 사용 하 여 다른 가상 컴퓨터의 공용 DNS names, hello 및 hello 트래픽 hello 인터넷을 통해 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f8e-112">hello virtual machines in a standalone cloud service communicate with other virtual machines by using hello other virtual machines’ public DNS names, and hello traffic travels over hello Internet.</span></span> <span data-ttu-id="97f8e-113">클라우드 서비스에에서 있으면 hello 가상 컴퓨터 가상 네트워크를 클라우드 서비스는 hello 인터넷을 통해 모든 트래픽을 전송 하지 않고 hello 가상 네트워크의 다른 모든 가상 컴퓨터와 통신할 수 있다는 점에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f8e-113">If a cloud service is in a virtual network, hello virtual machines in that cloud service can communicate with all other virtual machines in hello virtual network without sending any traffic over hello Internet.</span></span>

<span data-ttu-id="97f8e-114">배치 하는 경우 가상 컴퓨터에 hello 같은 독립 실행형 클라우드 서비스, 부하 분산을 계속 사용할 수 있습니다 및 가용성 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="97f8e-114">If you place your virtual machines in hello same standalone cloud service, you can still use load balancing and availability sets.</span></span> <span data-ttu-id="97f8e-115">자세한 내용은 참조 [부하 분산 가상 컴퓨터](../../virtual-machines-linux-load-balance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 및 [관리 가상 컴퓨터의 가용성을 hello](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="97f8e-115">For details, see [Load balancing virtual machines](../../virtual-machines-linux-load-balance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) and [Manage hello availability of virtual machines](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="97f8e-116">그러나 서브넷에 hello 가상 컴퓨터를 구성 하거나 독립 실행형 클라우드 서비스 tooyour 온-프레미스 네트워크 연결 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="97f8e-116">However, you can't organize hello virtual machines on subnets or connect a standalone cloud service tooyour on-premises network.</span></span> <span data-ttu-id="97f8e-117">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="97f8e-117">Here's an example:</span></span>

[!INCLUDE [virtual-machines-common-classic-connect-vms](../../../../includes/virtual-machines-common-classic-connect-vms.md)]

## <a name="next-steps"></a><span data-ttu-id="97f8e-118">다음 단계</span><span class="sxs-lookup"><span data-stu-id="97f8e-118">Next steps</span></span>
<span data-ttu-id="97f8e-119">가상 컴퓨터를 만든 후는 것이 좋습니다 너무[데이터 디스크 추가](attach-disk.md) 서비스 및 작업에 위치 toostore 데이터 갖도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="97f8e-119">After you create a virtual machine, it's a good idea too[add a data disk](attach-disk.md) so your services and workloads have a location toostore data.</span></span>
