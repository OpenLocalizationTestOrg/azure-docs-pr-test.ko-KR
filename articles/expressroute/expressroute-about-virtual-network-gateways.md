---
title: "ExpressRoute 가상 네트워크 게이트웨이 정보 | Microsoft 문서"
description: "ExpressRoute의 가상 네트워크 게이트웨이에 대해 알아봅니다."
services: expressroute
documentationcenter: na
author: cherylmc
manager: carmonm
editor: 
tags: azure-resource-manager, azure-service-management
ms.assetid: 7e0d9658-bc00-45b0-848f-f7a6da648635
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: cherylmc
ms.openlocfilehash: a6363fa380d0bab05d7500141cc6019d1d3f68b8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="about-virtual-network-gateways-for-expressroute"></a><span data-ttu-id="5ac38-103">ExpressRoute에 대한 가상 네트워크 게이트웨이 정보</span><span class="sxs-lookup"><span data-stu-id="5ac38-103">About virtual network gateways for ExpressRoute</span></span>
<span data-ttu-id="5ac38-104">가상 네트워크 게이트웨이는 Azure 가상 네트워크와 온-프레미스 위치 간에 네트워크 트래픽을 보내는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ac38-104">A virtual network gateway is used to send network traffic between Azure virtual networks and on-premises locations.</span></span> <span data-ttu-id="5ac38-105">ExpressRoute 연결을 구성할 때 가상 네트워크 게이트웨이 및 가상 네트워크 게이트웨이 연결을 만들고 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ac38-105">When you configure an ExpressRoute connection, you must create and configure a virtual network gateway and a virtual network gateway connection.</span></span>

<span data-ttu-id="5ac38-106">가상 네트워크 게이트웨이를 만들 때 몇 가지 설정을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5ac38-106">When you create a virtual network gateway, you specify several settings.</span></span> <span data-ttu-id="5ac38-107">필수 설정 중 하나에서는 ExpressRoute 또는 사이트 간 VPN 트래픽에 게이트웨이를 사용할지 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5ac38-107">One of the required settings specifies whether the gateway will be used for ExpressRoute or Site-to-Site VPN traffic.</span></span> <span data-ttu-id="5ac38-108">Resource Manager 배포 모델에서 이 설정은 '-GatewayType'입니다.</span><span class="sxs-lookup"><span data-stu-id="5ac38-108">In the Resource Manager deployment model, the setting is '-GatewayType'.</span></span>

<span data-ttu-id="5ac38-109">개인 연결을 통해 네트워크 트래픽을 전송하는 경우 'ExpressRoute' 게이트웨이 유형을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5ac38-109">When network traffic is sent on a private connection, you use the gateway type 'ExpressRoute'.</span></span> <span data-ttu-id="5ac38-110">이를 Express 경로 게이트웨이라고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ac38-110">This is also referred to as an ExpressRoute gateway.</span></span> <span data-ttu-id="5ac38-111">네트워크 트래픽을 공용 인터넷을 통해 암호화하여 전송하면 'Vpn' 게이트웨이 유형을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5ac38-111">When network traffic is sent encrypted across the public Internet, you use the gateway type 'Vpn'.</span></span> <span data-ttu-id="5ac38-112">이를 VPN Gateway라고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ac38-112">This is referred to as a VPN gateway.</span></span> <span data-ttu-id="5ac38-113">사이트 간, 지점 및 사이트 간, VNet 간 연결은 모두 VPN Gateway를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5ac38-113">Site-to-Site, Point-to-Site, and VNet-to-VNet connections all use a VPN gateway.</span></span>

<span data-ttu-id="5ac38-114">각각의 가상 네트워크에는 게이트웨이 유형당 하나의 가상 네트워크 게이트웨이가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ac38-114">Each virtual network can have only one virtual network gateway per gateway type.</span></span> <span data-ttu-id="5ac38-115">예를 들어 -GatewayType Vpn을 사용하는 하나의 가상 네트워크 게이트웨이와 -GatewayType Express 경로를 사용하는 하나의 가상 네트워크 게이트웨이가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ac38-115">For example, you can have one virtual network gateway that uses -GatewayType Vpn, and one that uses -GatewayType ExpressRoute.</span></span> <span data-ttu-id="5ac38-116">이 문서에서는 ExpressRoute 가상 네트워크 게이트웨이를 중점적으로 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="5ac38-116">This article focuses on the ExpressRoute virtual network gateway.</span></span>

## <span data-ttu-id="5ac38-117"><a name="gwsku"></a>게이트웨이 SKU</span><span class="sxs-lookup"><span data-stu-id="5ac38-117"><a name="gwsku"></a>Gateway SKUs</span></span>
[!INCLUDE [expressroute-gwsku-include](../../includes/expressroute-gwsku-include.md)]

<span data-ttu-id="5ac38-118">게이트웨이를 보다 강력한 게이트웨이 SKU로 업그레이드하려면 대부분의 경우 'Resize-AzureRmVirtualNetworkGateway' PowerShell cmdlet을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ac38-118">If you want to upgrade your gateway to a more powerful gateway SKU, in most cases you can use the 'Resize-AzureRmVirtualNetworkGateway' PowerShell cmdlet.</span></span> <span data-ttu-id="5ac38-119">표준 및 고성능 SKU로 업그레이드하는 경우에 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="5ac38-119">This will work for upgrades to Standard and HighPerformance SKUs.</span></span> <span data-ttu-id="5ac38-120">하지만 초고성능 SKU로 업그레이드하려면 게이트웨이를 다시 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ac38-120">However, to upgrade to the UltraPerformance SKU, you will need to recreate the gateway.</span></span>

### <span data-ttu-id="5ac38-121"><a name="aggthroughput"></a>게이트웨이 SKU에 의해 예상된 총 처리량</span><span class="sxs-lookup"><span data-stu-id="5ac38-121"><a name="aggthroughput"></a>Estimated aggregate throughput by gateway SKU</span></span>
<span data-ttu-id="5ac38-122">다음 테이블에서는 게이트웨이 형식과 예상 총 처리량을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5ac38-122">The following table shows the gateway types and the estimated aggregate throughput.</span></span> <span data-ttu-id="5ac38-123">이 표는 리소스 관리자 배포 모델과 클래식 배포 모델 모두에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ac38-123">This table applies to both the Resource Manager and classic deployment models.</span></span>

[!INCLUDE [expressroute-table-aggthroughput](../../includes/expressroute-table-aggtput-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="5ac38-124">응용 프로그램 처리량은 종단 간 대기 시간 및 응용 프로그램을 여는 트래픽 흐름 수와 같은 여러 요인에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="5ac38-124">Application throughput depends on multiple factors, such as the end-to-end latency, and the number of traffic flows the application opens.</span></span> <span data-ttu-id="5ac38-125">테이블의 숫자는 이상적인 환경에서 응용 프로그램이 이론상 수행할 수 있는 상한값을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="5ac38-125">The numbers in the table represent the upper limit that the application can theorectically achieve in an ideal environment.</span></span> 
> 
>

## <span data-ttu-id="5ac38-126"><a name="resources"></a>REST API 및 PowerShell cmdlet</span><span class="sxs-lookup"><span data-stu-id="5ac38-126"><a name="resources"></a>REST APIs and PowerShell cmdlets</span></span>
<span data-ttu-id="5ac38-127">가상 네트워크 게이트웨이 구성을 위해 REST API와 PowerShell cmdlet을 사용할 경우 추가 기술 리소스 및 특정 구문 요구 사항에 대해서는 다음 페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5ac38-127">For additional technical resources and specific syntax requirements when using REST APIs and PowerShell cmdlets for virtual network gateway configurations, see the following pages:</span></span>

| <span data-ttu-id="5ac38-128">**클래식**</span><span class="sxs-lookup"><span data-stu-id="5ac38-128">**Classic**</span></span> | <span data-ttu-id="5ac38-129">**리소스 관리자**</span><span class="sxs-lookup"><span data-stu-id="5ac38-129">**Resource Manager**</span></span> |
| --- | --- |
| [<span data-ttu-id="5ac38-130">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5ac38-130">PowerShell</span></span>](https://msdn.microsoft.com/library/mt270335.aspx) |[<span data-ttu-id="5ac38-131">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5ac38-131">PowerShell</span></span>](https://msdn.microsoft.com/library/mt163510.aspx) |
| [<span data-ttu-id="5ac38-132">REST API</span><span class="sxs-lookup"><span data-stu-id="5ac38-132">REST API</span></span>](https://msdn.microsoft.com/library/jj154113.aspx) |[<span data-ttu-id="5ac38-133">REST API</span><span class="sxs-lookup"><span data-stu-id="5ac38-133">REST API</span></span>](https://msdn.microsoft.com/library/mt163859.aspx) |

## <a name="next-steps"></a><span data-ttu-id="5ac38-134">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5ac38-134">Next steps</span></span>
<span data-ttu-id="5ac38-135">사용 가능한 연결 구성에 대한 자세한 내용은 [ExpressRoute 개요](expressroute-introduction.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5ac38-135">See [ExpressRoute Overview](expressroute-introduction.md) for more information about available connection configurations.</span></span> 

