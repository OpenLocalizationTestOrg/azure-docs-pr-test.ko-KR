---
title: "Hello 로컬 네트워크 게이트웨이 IP 주소 접두사 및 hello VPN 게이트웨이 IP 주소 수정 | Azure | PowerShell | Microsoft Docs"
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
ms.openlocfilehash: 1353598b39a97fae9bdb424505a5ae2560482654
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="modify-local-network-gateway-settings-using-powershell"></a><span data-ttu-id="5b73a-103">PowerShell을 사용하여 로컬 네트워크 게이트웨이 설정 수정</span><span class="sxs-lookup"><span data-stu-id="5b73a-103">Modify local network gateway settings using PowerShell</span></span>

<span data-ttu-id="5b73a-104">경우에 따라 로컬 네트워크 게이트웨이 AddressPrefix 또는 GatewayIPAddress에 대 한 hello 설정을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="5b73a-104">Sometimes hello settings for your local network gateway AddressPrefix or GatewayIPAddress change.</span></span> <span data-ttu-id="5b73a-105">이 문서에서는 어떻게 toomodify 로컬 네트워크 게이트웨이 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b73a-105">This article shows you how toomodify your local network gateway settings.</span></span> <span data-ttu-id="5b73a-106">또한 다른 메서드를 사용 하 여 hello 다음 목록에서에서 다른 옵션을 선택 하 여 이러한 설정을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b73a-106">You can also modify these settings using a different method by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="5b73a-107">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="5b73a-107">Azure portal</span></span>](vpn-gateway-modify-local-network-gateway-portal.md)
> * [<span data-ttu-id="5b73a-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5b73a-108">PowerShell</span></span>](vpn-gateway-modify-local-network-gateway.md)
> * [<span data-ttu-id="5b73a-109">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="5b73a-109">Azure CLI</span></span>](vpn-gateway-modify-local-network-gateway-cli.md)
>
>

## <span data-ttu-id="5b73a-110"><a name="before"></a>시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="5b73a-110"><a name="before"></a>Before you begin</span></span>

<span data-ttu-id="5b73a-111">Hello hello Azure 리소스 관리자 PowerShell cmdlet의 최신 버전을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b73a-111">Install hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="5b73a-112">참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azureps-cmdlets-docs) hello PowerShell cmdlet을 설치 하는 방법에 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b73a-112">See [How tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for more information about installing hello PowerShell cmdlets.</span></span>

## <span data-ttu-id="5b73a-113"><a name="ipaddprefix"></a>IP 주소 접두사 수정</span><span class="sxs-lookup"><span data-stu-id="5b73a-113"><a name="ipaddprefix"></a>Modify IP address prefixes</span></span>

[!INCLUDE [vpn-gateway-modify-ip-prefix-rm](../../includes/vpn-gateway-modify-ip-prefix-rm-include.md)]

## <span data-ttu-id="5b73a-114"><a name="gwip"></a>Hello 게이트웨이 IP 주소를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b73a-114"><a name="gwip"></a>Modify hello gateway IP address</span></span>

[!INCLUDE [vpn-gateway-modify-lng-gateway-ip-rm](../../includes/vpn-gateway-modify-lng-gateway-ip-rm-include.md)]

## <a name="next-steps"></a><span data-ttu-id="5b73a-115">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5b73a-115">Next steps</span></span>

<span data-ttu-id="5b73a-116">게이트웨이 연결을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b73a-116">You can verify your gateway connection.</span></span> <span data-ttu-id="5b73a-117">[게이트웨이 연결 확인](vpn-gateway-verify-connection-resource-manager.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5b73a-117">See [Verify a gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>