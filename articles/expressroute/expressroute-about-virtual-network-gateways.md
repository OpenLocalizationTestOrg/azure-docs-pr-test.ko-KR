---
title: "aaaAbout ExpressRoute 가상 네트워크 게이트웨이 | Microsoft Docs"
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
ms.openlocfilehash: 4daf4f96b4fadb00683d8e536e51734853008c50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="about-virtual-network-gateways-for-expressroute"></a><span data-ttu-id="f428d-103">ExpressRoute에 대한 가상 네트워크 게이트웨이 정보</span><span class="sxs-lookup"><span data-stu-id="f428d-103">About virtual network gateways for ExpressRoute</span></span>
<span data-ttu-id="f428d-104">가상 네트워크 게이트웨이에 사용 되는 Azure 가상 네트워크와 온-프레미스 위치 사이의 네트워크 트래픽을 toosend 합니다.</span><span class="sxs-lookup"><span data-stu-id="f428d-104">A virtual network gateway is used toosend network traffic between Azure virtual networks and on-premises locations.</span></span> <span data-ttu-id="f428d-105">ExpressRoute 연결을 구성할 때 가상 네트워크 게이트웨이 및 가상 네트워크 게이트웨이 연결을 만들고 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f428d-105">When you configure an ExpressRoute connection, you must create and configure a virtual network gateway and a virtual network gateway connection.</span></span>

<span data-ttu-id="f428d-106">가상 네트워크 게이트웨이를 만들 때 몇 가지 설정을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f428d-106">When you create a virtual network gateway, you specify several settings.</span></span> <span data-ttu-id="f428d-107">사이트 간 VPN 또는 express 경로도 트래픽에 대 한 hello 게이트웨이 사용할지 여부 필요한 hello 설정 중 하나를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f428d-107">One of hello required settings specifies whether hello gateway will be used for ExpressRoute or Site-to-Site VPN traffic.</span></span> <span data-ttu-id="f428d-108">Hello 설정을 hello 리소스 관리자 배포 모델에는 '-GatewayType'.</span><span class="sxs-lookup"><span data-stu-id="f428d-108">In hello Resource Manager deployment model, hello setting is '-GatewayType'.</span></span>

<span data-ttu-id="f428d-109">개인 연결 네트워크 트래픽을 전송 하는 경우 'ExpressRoute' hello 게이트웨이 유형을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f428d-109">When network traffic is sent on a private connection, you use hello gateway type 'ExpressRoute'.</span></span> <span data-ttu-id="f428d-110">참조 된 tooas express 경로 게이트웨이 이기도합니다.</span><span class="sxs-lookup"><span data-stu-id="f428d-110">This is also referred tooas an ExpressRoute gateway.</span></span> <span data-ttu-id="f428d-111">네트워크 트래픽을 암호화에서 전송 된 때 공용 인터넷 hello를 hello 게이트웨이 유형 'Vpn'를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f428d-111">When network traffic is sent encrypted across hello public Internet, you use hello gateway type 'Vpn'.</span></span> <span data-ttu-id="f428d-112">참조 된 tooas VPN 게이트웨이입니다.</span><span class="sxs-lookup"><span data-stu-id="f428d-112">This is referred tooas a VPN gateway.</span></span> <span data-ttu-id="f428d-113">사이트 간, 지점 및 사이트 간, VNet 간 연결은 모두 VPN Gateway를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f428d-113">Site-to-Site, Point-to-Site, and VNet-to-VNet connections all use a VPN gateway.</span></span>

<span data-ttu-id="f428d-114">각각의 가상 네트워크에는 게이트웨이 유형당 하나의 가상 네트워크 게이트웨이가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f428d-114">Each virtual network can have only one virtual network gateway per gateway type.</span></span> <span data-ttu-id="f428d-115">예를 들어 -GatewayType Vpn을 사용하는 하나의 가상 네트워크 게이트웨이와 -GatewayType Express 경로를 사용하는 하나의 가상 네트워크 게이트웨이가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f428d-115">For example, you can have one virtual network gateway that uses -GatewayType Vpn, and one that uses -GatewayType ExpressRoute.</span></span> <span data-ttu-id="f428d-116">이 문서는 hello ExpressRoute 가상 네트워크 게이트웨이에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="f428d-116">This article focuses on hello ExpressRoute virtual network gateway.</span></span>

## <span data-ttu-id="f428d-117"><a name="gwsku"></a>게이트웨이 SKU</span><span class="sxs-lookup"><span data-stu-id="f428d-117"><a name="gwsku"></a>Gateway SKUs</span></span>
[!INCLUDE [expressroute-gwsku-include](../../includes/expressroute-gwsku-include.md)]

<span data-ttu-id="f428d-118">원하는 tooupgrade 게이트웨이 tooa 더 강력 하는 경우 게이트웨이 SKU, 대부분의 경우 사용할 수 있습니다 hello ' 크기 조정 AzureRmVirtualNetworkGateway' PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f428d-118">If you want tooupgrade your gateway tooa more powerful gateway SKU, in most cases you can use hello 'Resize-AzureRmVirtualNetworkGateway' PowerShell cmdlet.</span></span> <span data-ttu-id="f428d-119">이 기능은 업그레이드 tooStandard 및 HighPerformance Sku에 대 한 작동 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f428d-119">This will work for upgrades tooStandard and HighPerformance SKUs.</span></span> <span data-ttu-id="f428d-120">그러나 tooupgrade toohello UltraPerformance SKU 해야 toorecreate hello 게이트웨이 합니다.</span><span class="sxs-lookup"><span data-stu-id="f428d-120">However, tooupgrade toohello UltraPerformance SKU, you will need toorecreate hello gateway.</span></span>

### <span data-ttu-id="f428d-121"><a name="aggthroughput"></a>게이트웨이 SKU에 의해 예상된 총 처리량</span><span class="sxs-lookup"><span data-stu-id="f428d-121"><a name="aggthroughput"></a>Estimated aggregate throughput by gateway SKU</span></span>
<span data-ttu-id="f428d-122">hello 다음 표에 hello 게이트웨이 유형 및 집계 처리량을 예상된 hello 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f428d-122">hello following table shows hello gateway types and hello estimated aggregate throughput.</span></span> <span data-ttu-id="f428d-123">이 테이블 tooboth hello 리소스 관리자 및 클래식 배포 모델을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="f428d-123">This table applies tooboth hello Resource Manager and classic deployment models.</span></span>

[!INCLUDE [expressroute-table-aggthroughput](../../includes/expressroute-table-aggtput-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="f428d-124">Hello 수가 트래픽 흐름 hello 응용 프로그램 열립니다 및 응용 프로그램 처리량 hello 종단 간 대기 시간 등의 여러 요인에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="f428d-124">Application throughput depends on multiple factors, such as hello end-to-end latency, and hello number of traffic flows hello application opens.</span></span> <span data-ttu-id="f428d-125">hello 숫자 hello 테이블 나타내는 hello 상한 hello 응용 프로그램 theorectically 수 있는 이상적인 환경에서 달성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f428d-125">hello numbers in hello table represent hello upper limit that hello application can theorectically achieve in an ideal environment.</span></span> 
> 
>

## <span data-ttu-id="f428d-126"><a name="resources"></a>REST API 및 PowerShell cmdlet</span><span class="sxs-lookup"><span data-stu-id="f428d-126"><a name="resources"></a>REST APIs and PowerShell cmdlets</span></span>
<span data-ttu-id="f428d-127">추가 기술 리소스 및 가상 네트워크 게이트웨이 구성에 대 한 REST Api 및 PowerShell cmdlet을 사용 하는 경우 특정 구문 요구 사항에 대 한 hello 다음 페이지를 참조:</span><span class="sxs-lookup"><span data-stu-id="f428d-127">For additional technical resources and specific syntax requirements when using REST APIs and PowerShell cmdlets for virtual network gateway configurations, see hello following pages:</span></span>

| <span data-ttu-id="f428d-128">**클래식**</span><span class="sxs-lookup"><span data-stu-id="f428d-128">**Classic**</span></span> | <span data-ttu-id="f428d-129">**리소스 관리자**</span><span class="sxs-lookup"><span data-stu-id="f428d-129">**Resource Manager**</span></span> |
| --- | --- |
| [<span data-ttu-id="f428d-130">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f428d-130">PowerShell</span></span>](https://msdn.microsoft.com/library/mt270335.aspx) |[<span data-ttu-id="f428d-131">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f428d-131">PowerShell</span></span>](https://msdn.microsoft.com/library/mt163510.aspx) |
| [<span data-ttu-id="f428d-132">REST API</span><span class="sxs-lookup"><span data-stu-id="f428d-132">REST API</span></span>](https://msdn.microsoft.com/library/jj154113.aspx) |[<span data-ttu-id="f428d-133">REST API</span><span class="sxs-lookup"><span data-stu-id="f428d-133">REST API</span></span>](https://msdn.microsoft.com/library/mt163859.aspx) |

## <a name="next-steps"></a><span data-ttu-id="f428d-134">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f428d-134">Next steps</span></span>
<span data-ttu-id="f428d-135">사용 가능한 연결 구성에 대한 자세한 내용은 [ExpressRoute 개요](expressroute-introduction.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f428d-135">See [ExpressRoute Overview](expressroute-introduction.md) for more information about available connection configurations.</span></span> 

