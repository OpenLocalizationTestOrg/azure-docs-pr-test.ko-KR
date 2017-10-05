---
title: "VPN Gateway 연결 확인 | Microsoft Docs"
description: "이 문서에서는 가상 네트워크 VPN Gateway 연결을 확인하는 방법을 보여 줍니다."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 7e3d1043-caa9-4472-96d3-832f4e2c91ee
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/16/2017
ms.author: cherylmc
ms.openlocfilehash: b2d702ecdd5e1fca342e7c84c6e75339097f0bcd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="verify-a-vpn-gateway-connection"></a><span data-ttu-id="3b3c6-103">VPN Gateway 연결 확인</span><span class="sxs-lookup"><span data-stu-id="3b3c6-103">Verify a VPN Gateway connection</span></span>

<span data-ttu-id="3b3c6-104">이 문서에서는 클래식 및 Resource Manager 배포 모델에 대한 VPN Gateway 연결을 확인하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3b3c6-104">This article shows you how to verify a VPN gateway connection for both the classic and Resource Manager deployment models.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="3b3c6-105">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="3b3c6-105">Azure portal</span></span>

[!INCLUDE [Azure portal](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <a name="powershell"></a><span data-ttu-id="3b3c6-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3b3c6-106">PowerShell</span></span>

<span data-ttu-id="3b3c6-107">PowerShell을 사용하여 Resource Manager 배포 모델에 대한 VPN Gateway 연결을 확인하려면 최신 버전의 [Azure Resource Manager PowerShell cmdlet](/powershell/azure/overview)을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="3b3c6-107">To verify a VPN gateway connection for the Resource Manager deployment model using PowerShell, install the latest version of the [Azure Resource Manager PowerShell cmdlets](/powershell/azure/overview).</span></span>

[!INCLUDE [PowerShell](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="azure-cli"></a><span data-ttu-id="3b3c6-108">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="3b3c6-108">Azure CLI</span></span>

<span data-ttu-id="3b3c6-109">Azure CLI를 사용하여 Resource Manager 배포 모델에 대한 VPN Gateway 연결을 확인하려면 최신 버전의 [CLI 명령](https://docs.microsoft.com/cli/azure/install-azure-cli)(2.0 이상)을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="3b3c6-109">To verify a VPN gateway connection for the Resource Manager deployment model using Azure CLI, install the latest version of the [CLI commands](https://docs.microsoft.com/cli/azure/install-azure-cli) (2.0 or later).</span></span>

[!INCLUDE [CLI](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]


## <a name="azure-portal-classic"></a><span data-ttu-id="3b3c6-110">Azure Portal(클래식)</span><span class="sxs-lookup"><span data-stu-id="3b3c6-110">Azure portal (classic)</span></span>

[!INCLUDE [Azure portal](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]

## <a name="powershell-classic"></a><span data-ttu-id="3b3c6-111">PowerShell(클래식)</span><span class="sxs-lookup"><span data-stu-id="3b3c6-111">PowerShell (classic)</span></span>

<span data-ttu-id="3b3c6-112">PowerShell을 사용하여 클래식 배포 모델에 대한 VPN Gateway 연결을 확인하려면 최신 버전의 Azure PowerShell cmdlet을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="3b3c6-112">To verify your VPN gateway connection for the classic deployment model using PowerShell, install the latest versions of the Azure PowerShell cmdlets.</span></span> <span data-ttu-id="3b3c6-113">[Service Management](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0) 모듈을 다운로드하여 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b3c6-113">Be sure to download and install the [Service Management](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0) module.</span></span> <span data-ttu-id="3b3c6-114">'Add-AzureAccount'를 사용하여 클래식 배포 모델에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="3b3c6-114">Use 'Add-AzureAccount' to log in to the classic deployment model.</span></span>

[!INCLUDE [Classic PowerShell](../../includes/vpn-gateway-verify-connection-ps-classic-include.md)]

## <a name="next-steps"></a><span data-ttu-id="3b3c6-115">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3b3c6-115">Next steps</span></span>

* <span data-ttu-id="3b3c6-116">가상 네트워크에 가상 컴퓨터를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b3c6-116">You can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="3b3c6-117">단계는 [가상 컴퓨터 만들기](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b3c6-117">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>