---
title: "로컬 네트워크 게이트웨이 IP 주소 접두사 및 VPN Gateway IP 주소 수정 | Azure | Portal | Microsoft Docs"
description: "이 문서는 Azure Portal을 사용하여 로컬 네트워크 게이트웨이에 대한 IP 주소 접두사를 변경하는 방법을 안내합니다."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: cherylmc
ms.openlocfilehash: bdd6f90fe97408bd45a72adf58bfdc190207de46
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="modify-local-network-gateway-settings-using-the-azure-portal"></a><span data-ttu-id="9a3e0-103">Azure Portal을 사용하여 로컬 네트워크 게이트웨이 설정 수정</span><span class="sxs-lookup"><span data-stu-id="9a3e0-103">Modify local network gateway settings using the Azure portal</span></span>

<span data-ttu-id="9a3e0-104">때로는 로컬 네트워크 게이트웨이 AddressPrefix 또는 GatewayIPAddress에 대한 설정을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="9a3e0-104">Sometimes the settings for your local network gateway AddressPrefix or GatewayIPAddress change.</span></span> <span data-ttu-id="9a3e0-105">이 문서는 로컬 네트워크 게이트웨이 설정을 수정하는 방법을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="9a3e0-105">This article shows you how to modify your local network gateway settings.</span></span> <span data-ttu-id="9a3e0-106">다음 목록에서 다른 옵션을 선택해 다른 방법으로 이러한 설정을 수정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a3e0-106">You can also modify these settings using a different method by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="9a3e0-107">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="9a3e0-107">Azure portal</span></span>](vpn-gateway-modify-local-network-gateway-portal.md)
> * [<span data-ttu-id="9a3e0-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9a3e0-108">PowerShell</span></span>](vpn-gateway-modify-local-network-gateway.md)
> * [<span data-ttu-id="9a3e0-109">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="9a3e0-109">Azure CLI</span></span>](vpn-gateway-modify-local-network-gateway-cli.md)
>
>


## <span data-ttu-id="9a3e0-110"><a name="ipaddprefix"></a>IP 주소 접두사 수정</span><span class="sxs-lookup"><span data-stu-id="9a3e0-110"><a name="ipaddprefix"></a>Modify IP address prefixes</span></span>

<span data-ttu-id="9a3e0-111">IP 주소 접두사를 수정하는 경우 수행하는 단계는 로컬 네트워크 게이트웨이에 에 연결이 있는지 여부에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="9a3e0-111">When you modify IP address prefixes, the steps you follow depend on whether your local network gateway has a connection.</span></span>

[!INCLUDE [modify prefix](../../includes/vpn-gateway-modify-ip-prefix-portal-include.md)]

## <span data-ttu-id="9a3e0-112"><a name="gwip"></a>게이트웨이 IP 주소 수정</span><span class="sxs-lookup"><span data-stu-id="9a3e0-112"><a name="gwip"></a>Modify the gateway IP address</span></span>

<span data-ttu-id="9a3e0-113">연결하려는 VPN 장치의 공용 IP 주소가 변경된 경우 해당 변경 내용을 반영하도록 로컬 네트워크 게이트웨이를 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a3e0-113">If the VPN device that you want to connect to has changed its public IP address, you need to modify the local network gateway to reflect that change.</span></span> <span data-ttu-id="9a3e0-114">공용 IP 주소를 변경하는 경우 수행하는 단계는 로컬 네트워크 게이트웨이에 에 연결이 있는지 여부에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="9a3e0-114">When you change the public IP address, the steps you follow depend on whether your local network gateway has a connection.</span></span>

[!INCLUDE [modify gateway IP](../../includes/vpn-gateway-modify-lng-gateway-ip-portal-include.md)]

## <a name="next-steps"></a><span data-ttu-id="9a3e0-115">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9a3e0-115">Next steps</span></span>

<span data-ttu-id="9a3e0-116">게이트웨이 연결을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a3e0-116">You can verify your gateway connection.</span></span> <span data-ttu-id="9a3e0-117">[게이트웨이 연결 확인](vpn-gateway-verify-connection-resource-manager.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9a3e0-117">See [Verify a gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>