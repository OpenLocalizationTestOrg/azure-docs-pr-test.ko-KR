---
title: "로컬 네트워크 게이트웨이 IP 주소 접두사 및 VPN Gateway IP 주소 수정 | Azure | PowerShell | Microsoft Docs"
description: "이 문서에서는 PowerShell을 사용하여 로컬 네트워크 게이트웨이에 대한 IP 주소 접두사를 변경하는 방법을 안내합니다."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8c7db48f-d09a-44e7-836f-1fb6930389df
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: cherylmc
ms.openlocfilehash: 2a095b96a8c352abeca72640d37c0d629b447763
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="modify-local-network-gateway-settings-using-powershell"></a><span data-ttu-id="f9c84-103">PowerShell을 사용하여 로컬 네트워크 게이트웨이 설정 수정</span><span class="sxs-lookup"><span data-stu-id="f9c84-103">Modify local network gateway settings using PowerShell</span></span>

<span data-ttu-id="f9c84-104">때로는 로컬 네트워크 게이트웨이 AddressPrefix 또는 GatewayIPAddress에 대한 설정을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="f9c84-104">Sometimes the settings for your local network gateway AddressPrefix or GatewayIPAddress change.</span></span> <span data-ttu-id="f9c84-105">이 문서는 로컬 네트워크 게이트웨이 설정을 수정하는 방법을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="f9c84-105">This article shows you how to modify your local network gateway settings.</span></span> <span data-ttu-id="f9c84-106">다음 목록에서 다른 옵션을 선택해 다른 방법으로 이러한 설정을 수정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9c84-106">You can also modify these settings using a different method by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f9c84-107">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="f9c84-107">Azure portal</span></span>](vpn-gateway-modify-local-network-gateway-portal.md)
> * [<span data-ttu-id="f9c84-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f9c84-108">PowerShell</span></span>](vpn-gateway-modify-local-network-gateway.md)
> * [<span data-ttu-id="f9c84-109">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="f9c84-109">Azure CLI</span></span>](vpn-gateway-modify-local-network-gateway-cli.md)
>
>

## <span data-ttu-id="f9c84-110"><a name="before"></a>시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="f9c84-110"><a name="before"></a>Before you begin</span></span>

<span data-ttu-id="f9c84-111">최신 버전의 Azure Resource Manager PowerShell cmdlet을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f9c84-111">Install the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="f9c84-112">PowerShell cmdlet 설치에 대한 자세한 내용은 [Azure PowerShell 설치 및 구성 방법](/powershell/azureps-cmdlets-docs) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f9c84-112">See [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for more information about installing the PowerShell cmdlets.</span></span>

## <span data-ttu-id="f9c84-113"><a name="ipaddprefix"></a>IP 주소 접두사 수정</span><span class="sxs-lookup"><span data-stu-id="f9c84-113"><a name="ipaddprefix"></a>Modify IP address prefixes</span></span>

[!INCLUDE [vpn-gateway-modify-ip-prefix-rm](../../includes/vpn-gateway-modify-ip-prefix-rm-include.md)]

## <span data-ttu-id="f9c84-114"><a name="gwip"></a>게이트웨이 IP 주소 수정</span><span class="sxs-lookup"><span data-stu-id="f9c84-114"><a name="gwip"></a>Modify the gateway IP address</span></span>

[!INCLUDE [vpn-gateway-modify-lng-gateway-ip-rm](../../includes/vpn-gateway-modify-lng-gateway-ip-rm-include.md)]

## <a name="next-steps"></a><span data-ttu-id="f9c84-115">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f9c84-115">Next steps</span></span>

<span data-ttu-id="f9c84-116">게이트웨이 연결을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9c84-116">You can verify your gateway connection.</span></span> <span data-ttu-id="f9c84-117">[게이트웨이 연결 확인](vpn-gateway-verify-connection-resource-manager.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f9c84-117">See [Verify a gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>