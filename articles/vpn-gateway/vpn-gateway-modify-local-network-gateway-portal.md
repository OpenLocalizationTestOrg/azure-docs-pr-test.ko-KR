---
title: "Hello 로컬 네트워크 게이트웨이 IP 주소 접두사 및 hello VPN 게이트웨이 IP 주소 수정 | Azure | 포털 | Microsoft Docs"
description: "이 문서 hello Azure 포털을 사용 하 여 로컬 네트워크 게이트웨이 IP 주소 접두사를 변경 하지 안내 합니다."
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
ms.openlocfilehash: 001df7b748ccc234d87aab3501a4f0e4ddfe60f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="modify-local-network-gateway-settings-using-hello-azure-portal"></a><span data-ttu-id="a0f0e-103">Hello Azure 포털을 사용 하 여 로컬 네트워크 게이트웨이 설정을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0f0e-103">Modify local network gateway settings using hello Azure portal</span></span>

<span data-ttu-id="a0f0e-104">경우에 따라 로컬 네트워크 게이트웨이 AddressPrefix 또는 GatewayIPAddress에 대 한 hello 설정을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="a0f0e-104">Sometimes hello settings for your local network gateway AddressPrefix or GatewayIPAddress change.</span></span> <span data-ttu-id="a0f0e-105">이 문서에서는 어떻게 toomodify 로컬 네트워크 게이트웨이 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0f0e-105">This article shows you how toomodify your local network gateway settings.</span></span> <span data-ttu-id="a0f0e-106">또한 다른 메서드를 사용 하 여 hello 다음 목록에서에서 다른 옵션을 선택 하 여 이러한 설정을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0f0e-106">You can also modify these settings using a different method by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="a0f0e-107">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="a0f0e-107">Azure portal</span></span>](vpn-gateway-modify-local-network-gateway-portal.md)
> * [<span data-ttu-id="a0f0e-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a0f0e-108">PowerShell</span></span>](vpn-gateway-modify-local-network-gateway.md)
> * [<span data-ttu-id="a0f0e-109">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a0f0e-109">Azure CLI</span></span>](vpn-gateway-modify-local-network-gateway-cli.md)
>
>


## <span data-ttu-id="a0f0e-110"><a name="ipaddprefix"></a>IP 주소 접두사 수정</span><span class="sxs-lookup"><span data-stu-id="a0f0e-110"><a name="ipaddprefix"></a>Modify IP address prefixes</span></span>

<span data-ttu-id="a0f0e-111">IP 주소 접두사를 수정 하는 경우 수행 해야 하는 hello 단계 로컬 네트워크 게이트웨이 연결에 있는지 여부에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="a0f0e-111">When you modify IP address prefixes, hello steps you follow depend on whether your local network gateway has a connection.</span></span>

[!INCLUDE [modify prefix](../../includes/vpn-gateway-modify-ip-prefix-portal-include.md)]

## <span data-ttu-id="a0f0e-112"><a name="gwip"></a>Hello 게이트웨이 IP 주소를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0f0e-112"><a name="gwip"></a>Modify hello gateway IP address</span></span>

<span data-ttu-id="a0f0e-113">원하는 tooconnect toohas hello VPN 장치에 공용 IP 주소 변경 된 경우 toomodify hello 로컬 네트워크 게이트웨이 tooreflect 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0f0e-113">If hello VPN device that you want tooconnect toohas changed its public IP address, you need toomodify hello local network gateway tooreflect that change.</span></span> <span data-ttu-id="a0f0e-114">Hello 공용 IP 주소를 변경 하면 수행 해야 하는 hello 단계 로컬 네트워크 게이트웨이 연결에 있는지 여부에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="a0f0e-114">When you change hello public IP address, hello steps you follow depend on whether your local network gateway has a connection.</span></span>

[!INCLUDE [modify gateway IP](../../includes/vpn-gateway-modify-lng-gateway-ip-portal-include.md)]

## <a name="next-steps"></a><span data-ttu-id="a0f0e-115">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a0f0e-115">Next steps</span></span>

<span data-ttu-id="a0f0e-116">게이트웨이 연결을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0f0e-116">You can verify your gateway connection.</span></span> <span data-ttu-id="a0f0e-117">[게이트웨이 연결 확인](vpn-gateway-verify-connection-resource-manager.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a0f0e-117">See [Verify a gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>