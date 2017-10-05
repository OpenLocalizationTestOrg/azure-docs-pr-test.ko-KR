---
title: "로컬 네트워크 게이트웨이 IP 주소 접두사 및 VPN Gateway IP 주소 수정 | Azure | CLI | Microsoft Docs"
description: "이 문서에서는 Azure CLI를 사용하여 로컬 네트워크 게이트웨이에 대한 IP 주소 접두사를 변경하는 방법을 안내합니다."
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
ms.openlocfilehash: 7db1ad970ebb93d46d5a861f9a9b27bf121531a3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="modify-local-network-gateway-settings-using-the-azure-cli"></a><span data-ttu-id="699a2-103">Azure CLI를 사용하여 로컬 네트워크 게이트웨이 설정 수정</span><span class="sxs-lookup"><span data-stu-id="699a2-103">Modify local network gateway settings using the Azure CLI</span></span>

<span data-ttu-id="699a2-104">때때로 로컬 네트워크 게이트웨이 주소 접두사 또는 게이트웨이 IP 주소에 대한 설정이 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="699a2-104">Sometimes the settings for your local network gateway Address Prefix or Gateway IP Address change.</span></span> <span data-ttu-id="699a2-105">이 문서는 로컬 네트워크 게이트웨이 설정을 수정하는 방법을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="699a2-105">This article shows you how to modify your local network gateway settings.</span></span> <span data-ttu-id="699a2-106">다음 목록에서 다른 옵션을 선택해 다른 방법으로 이러한 설정을 수정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="699a2-106">You can also modify these settings using a different method by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="699a2-107">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="699a2-107">Azure portal</span></span>](vpn-gateway-modify-local-network-gateway-portal.md)
> * [<span data-ttu-id="699a2-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="699a2-108">PowerShell</span></span>](vpn-gateway-modify-local-network-gateway.md)
> * [<span data-ttu-id="699a2-109">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="699a2-109">Azure CLI</span></span>](vpn-gateway-modify-local-network-gateway-cli.md)
>
>

## <span data-ttu-id="699a2-110"><a name="before"></a>시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="699a2-110"><a name="before"></a>Before you begin</span></span>

<span data-ttu-id="699a2-111">최신 버전의 CLI 명령(2.0 이상)을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="699a2-111">Install the latest version of the CLI commands (2.0 or later).</span></span> <span data-ttu-id="699a2-112">CLI 명령을 설치하는 방법에 대한 자세한 내용은 [Azure CLI 2.0 설치](https://docs.microsoft.com/cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="699a2-112">For information about installing the CLI commands, see [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

[!INCLUDE [CLI-login](../../includes/vpn-gateway-cli-login-include.md)]

## <span data-ttu-id="699a2-113"><a name="ipaddprefix"></a>IP 주소 접두사 수정</span><span class="sxs-lookup"><span data-stu-id="699a2-113"><a name="ipaddprefix"></a>Modify IP address prefixes</span></span>

[!INCLUDE [modify-prefix](../../includes/vpn-gateway-modify-ip-prefix-cli-include.md)]

## <span data-ttu-id="699a2-114"><a name="gwip"></a>게이트웨이 IP 주소 수정</span><span class="sxs-lookup"><span data-stu-id="699a2-114"><a name="gwip"></a>Modify the gateway IP address</span></span>

[!INCLUDE [modify-gateway-IP](../../includes/vpn-gateway-modify-lng-gateway-ip-cli-include.md)]

## <a name="next-steps"></a><span data-ttu-id="699a2-115">다음 단계</span><span class="sxs-lookup"><span data-stu-id="699a2-115">Next steps</span></span>

<span data-ttu-id="699a2-116">게이트웨이 연결을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="699a2-116">You can verify your gateway connection.</span></span> <span data-ttu-id="699a2-117">[게이트웨이 연결 확인](vpn-gateway-verify-connection-resource-manager.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="699a2-117">See [Verify a gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>

