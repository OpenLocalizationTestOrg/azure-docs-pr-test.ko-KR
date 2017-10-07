---
title: "Azure 네트워크 감시자 다음 홉-Azure CLI 2.0 aaaFind 다음 홉 | Microsoft Docs"
description: "이 문서는 어떤 hello 다음 홉 형식 및 Azure CLI를 사용 하 여 다음 홉 ip 주소를 사용 하 여를 찾는 방법을 설명 합니다."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 0700c274-3e0d-4dca-acfa-3ceac8990613
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 77c2bde51274bd5c64e7a2467f95139af620ca30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-azure-network-watcher-using-azure-cli-20"></a><span data-ttu-id="5987b-103">어떤 hello 다음 홉 형식이 hello 다음 홉 기능을 사용 하는 Azure CLI 2.0을 사용 하 여 Azure 네트워크 감시자 확인</span><span class="sxs-lookup"><span data-stu-id="5987b-103">Find out what hello next hop type is using hello Next Hop capability in Azure Network Watcher using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="5987b-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="5987b-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="5987b-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5987b-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="5987b-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="5987b-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="5987b-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="5987b-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="5987b-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="5987b-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="5987b-109">다음 홉 hello 기능을 제공 하는 네트워크 감시자의 기능을 가져오고 hello 다음 홉 형식이 지정 된 가상 컴퓨터를 기반으로 하는 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="5987b-109">Next hop is a feature of Network Watcher that provides hello ability get hello next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="5987b-110">이 기능은 가상 컴퓨터를 종료 하는 트래픽이 게이트웨이, 인터넷 또는 가상 네트워크 tooget tooits 대상에서 이동 하는 경우를 결정 하는 데 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5987b-110">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks tooget tooits destination.</span></span>

<span data-ttu-id="5987b-111">이 문서에서는 Windows, Mac 및 Linux에 대 한 사용 하지 않는 hello 리소스 관리 배포 모델, Azure CLI 2.0에 대 한 우리의 차세대 CLI 합니다.</span><span class="sxs-lookup"><span data-stu-id="5987b-111">This article uses our next generation CLI for hello resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="5987b-112">이 문서의 단계를 tooperform hello, 너무 필요한[Mac, Linux 및 Windows Azure CLI ()에 대 한 hello Azure 명령줄 인터페이스 설치](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2)합니다.</span><span class="sxs-lookup"><span data-stu-id="5987b-112">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="5987b-113">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="5987b-113">Before you begin</span></span>

<span data-ttu-id="5987b-114">이 시나리오에서는 Azure CLI toofind hello 다음 홉 형식이 hello 및 IP 주소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5987b-114">In this scenario, you will use hello Azure CLI toofind hello next hop type and IP address.</span></span>

<span data-ttu-id="5987b-115">이 시나리오에서는 hello 단계에 따라 이미 가정 [네트워크 감시자를 만들](network-watcher-create.md) toocreate 네트워크 감시자 합니다.</span><span class="sxs-lookup"><span data-stu-id="5987b-115">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span> <span data-ttu-id="5987b-116">hello 시나리오는 또한 적합 한 가상 컴퓨터가 리소스 그룹 사용 toobe 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5987b-116">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="5987b-117">시나리오</span><span class="sxs-lookup"><span data-stu-id="5987b-117">Scenario</span></span>

<span data-ttu-id="5987b-118">이 문서에서 설명 하는 hello 시나리오는 다음 홉 hello 다음 홉 형식 및 리소스에 대 한 IP 주소를 확인 하는 네트워크 감시자의 기능을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5987b-118">hello scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out hello next hop type and IP address for a resource.</span></span> <span data-ttu-id="5987b-119">다음 홉에 대 한 자세한 toolearn 방문 [다음 홉 개요](network-watcher-next-hop-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5987b-119">toolearn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>


## <a name="get-next-hop"></a><span data-ttu-id="5987b-120">다음 홉 가져오기</span><span class="sxs-lookup"><span data-stu-id="5987b-120">Get Next Hop</span></span>

<span data-ttu-id="5987b-121">hello 이라고 tooget hello 다음 홉 `az network watcher show-next-hop` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5987b-121">tooget hello next hop we call hello `az network watcher show-next-hop` cmdlet.</span></span> <span data-ttu-id="5987b-122">Hello cmdlet hello 네트워크 감시자 리소스 그룹, hello NetworkWatcher, 가상 컴퓨터 Id, 원본 IP 주소 및 대상 IP 주소 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="5987b-122">We pass hello cmdlet hello Network Watcher resource group, hello NetworkWatcher, virtual machine Id, source IP address, and destination IP address.</span></span> <span data-ttu-id="5987b-123">이 예제에서는 hello 대상 IP 주소는 다른 가상 네트워크에 VM tooa 합니다.</span><span class="sxs-lookup"><span data-stu-id="5987b-123">In this example, hello destination IP address is tooa VM in another virtual network.</span></span> <span data-ttu-id="5987b-124">Hello 두 가상 네트워크 간의 가상 네트워크 게이트웨이는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5987b-124">There is a virtual network gateway between hello two virtual networks.</span></span>

<span data-ttu-id="5987b-125">하지 않은 아직 설치 하 고 최신 hello 구성 [Azure CLI 2.0](/cli/azure/install-az-cli2) tooan Azure 계정을 사용 하 여 로그인 [az 로그인](/cli/azure/#login)합니다.</span><span class="sxs-lookup"><span data-stu-id="5987b-125">If you haven't yet, install and configure hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="5987b-126">Hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5987b-126">Then run hello following command:</span></span>

```azurecli
az network watcher show-next-hop --resource-group <resourcegroupName> --vm <vmNameorID> --source-ip <source-ip> --dest-ip <destination-ip>

```

> [!NOTE]
<span data-ttu-id="5987b-127">Hello Nic의 IP 전달이 사용 VM hello에 여러 Nic를 다음 NIC 매개 변수 hello (-i nic id)를 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5987b-127">If hello VM has multiple NICs and IP forwarding is enabled on any of hello NICs, then hello NIC parameter (-i nic-id) must be specified.</span></span> <span data-ttu-id="5987b-128">그렇지 않은 경우 선택적입니다.</span><span class="sxs-lookup"><span data-stu-id="5987b-128">Otherwise it is optional.</span></span>

## <a name="review-results"></a><span data-ttu-id="5987b-129">결과 검토</span><span class="sxs-lookup"><span data-stu-id="5987b-129">Review results</span></span>

<span data-ttu-id="5987b-130">완료 되 면 hello 결과가 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5987b-130">When complete, hello results are provided.</span></span> <span data-ttu-id="5987b-131">hello 다음 홉 IP 주소는 리소스의 hello 형식을 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5987b-131">hello next hop IP address is returned as well as hello type of resource it is.</span></span>

```azurecli
{
    "nextHopIpAddress": null,
    "nextHopType": "Internet",
    "routeTableId": "System Route"
}
```

<span data-ttu-id="5987b-132">hello 다음 목록은 hello 현재 사용 가능한 NextHopType 값.</span><span class="sxs-lookup"><span data-stu-id="5987b-132">hello following list shows hello currently available NextHopType values:</span></span>

<span data-ttu-id="5987b-133">**다음 홉 유형**</span><span class="sxs-lookup"><span data-stu-id="5987b-133">**Next Hop Type**</span></span>

* <span data-ttu-id="5987b-134">인터넷</span><span class="sxs-lookup"><span data-stu-id="5987b-134">Internet</span></span>
* <span data-ttu-id="5987b-135">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="5987b-135">VirtualAppliance</span></span>
* <span data-ttu-id="5987b-136">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="5987b-136">VirtualNetworkGateway</span></span>
* <span data-ttu-id="5987b-137">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="5987b-137">VnetLocal</span></span>
* <span data-ttu-id="5987b-138">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="5987b-138">HyperNetGateway</span></span>
* <span data-ttu-id="5987b-139">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="5987b-139">VnetPeering</span></span>
* <span data-ttu-id="5987b-140">없음</span><span class="sxs-lookup"><span data-stu-id="5987b-140">None</span></span>

## <a name="next-steps"></a><span data-ttu-id="5987b-141">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5987b-141">Next steps</span></span>

<span data-ttu-id="5987b-142">자세한 내용은 방법 tooreview 방문 하 여 프로그래밍 방식으로 네트워크 보안 그룹 설정을 [NSG 감사 네트워크 감시자를](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="5987b-142">Learn how tooreview your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span></span>
