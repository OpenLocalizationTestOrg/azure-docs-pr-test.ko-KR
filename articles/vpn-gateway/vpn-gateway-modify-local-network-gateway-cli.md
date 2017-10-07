---
title: "Hello 로컬 네트워크 게이트웨이 IP 주소 접두사 및 hello VPN 게이트웨이 IP 주소 수정 | Azure | CLI | Microsoft Docs"
description: "이 문서 hello Azure CLI를 사용 하 여 로컬 네트워크 게이트웨이 IP 주소 접두사를 변경 하지 안내 합니다."
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
ms.openlocfilehash: 4b8bbf3e9d3d42ac2d12f87360fa0a4134c57a21
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="modify-local-network-gateway-settings-using-hello-azure-cli"></a><span data-ttu-id="4cdd3-103">Hello Azure CLI를 사용 하 여 로컬 네트워크 게이트웨이 설정을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cdd3-103">Modify local network gateway settings using hello Azure CLI</span></span>

<span data-ttu-id="4cdd3-104">경우에 따라 로컬 네트워크 게이트웨이 주소 접두사 또는 게이트웨이 IP 주소에 대 한 hello 설정을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="4cdd3-104">Sometimes hello settings for your local network gateway Address Prefix or Gateway IP Address change.</span></span> <span data-ttu-id="4cdd3-105">이 문서에서는 어떻게 toomodify 로컬 네트워크 게이트웨이 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cdd3-105">This article shows you how toomodify your local network gateway settings.</span></span> <span data-ttu-id="4cdd3-106">또한 다른 메서드를 사용 하 여 hello 다음 목록에서에서 다른 옵션을 선택 하 여 이러한 설정을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cdd3-106">You can also modify these settings using a different method by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="4cdd3-107">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="4cdd3-107">Azure portal</span></span>](vpn-gateway-modify-local-network-gateway-portal.md)
> * [<span data-ttu-id="4cdd3-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4cdd3-108">PowerShell</span></span>](vpn-gateway-modify-local-network-gateway.md)
> * [<span data-ttu-id="4cdd3-109">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="4cdd3-109">Azure CLI</span></span>](vpn-gateway-modify-local-network-gateway-cli.md)
>
>

## <span data-ttu-id="4cdd3-110"><a name="before"></a>시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="4cdd3-110"><a name="before"></a>Before you begin</span></span>

<span data-ttu-id="4cdd3-111">Hello hello CLI 명령 (2.0 이상)의 최신 버전을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cdd3-111">Install hello latest version of hello CLI commands (2.0 or later).</span></span> <span data-ttu-id="4cdd3-112">Hello CLI 명령 설치에 대 한 정보를 참조 하십시오. [Azure CLI 2.0 설치](https://docs.microsoft.com/cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="4cdd3-112">For information about installing hello CLI commands, see [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

[!INCLUDE [CLI-login](../../includes/vpn-gateway-cli-login-include.md)]

## <span data-ttu-id="4cdd3-113"><a name="ipaddprefix"></a>IP 주소 접두사 수정</span><span class="sxs-lookup"><span data-stu-id="4cdd3-113"><a name="ipaddprefix"></a>Modify IP address prefixes</span></span>

[!INCLUDE [modify-prefix](../../includes/vpn-gateway-modify-ip-prefix-cli-include.md)]

## <span data-ttu-id="4cdd3-114"><a name="gwip"></a>Hello 게이트웨이 IP 주소를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cdd3-114"><a name="gwip"></a>Modify hello gateway IP address</span></span>

[!INCLUDE [modify-gateway-IP](../../includes/vpn-gateway-modify-lng-gateway-ip-cli-include.md)]

## <a name="next-steps"></a><span data-ttu-id="4cdd3-115">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4cdd3-115">Next steps</span></span>

<span data-ttu-id="4cdd3-116">게이트웨이 연결을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cdd3-116">You can verify your gateway connection.</span></span> <span data-ttu-id="4cdd3-117">[게이트웨이 연결 확인](vpn-gateway-verify-connection-resource-manager.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4cdd3-117">See [Verify a gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>

