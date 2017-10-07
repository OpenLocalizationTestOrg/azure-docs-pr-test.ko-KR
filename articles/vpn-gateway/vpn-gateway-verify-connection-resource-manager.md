---
title: "VPN 게이트웨이 연결 aaaVerify | Microsoft Docs"
description: "이 문서에서는 tooverify a 가상 네트워크 VPN 게이트웨이 연결 하는 방법을 설명 합니다."
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
ms.openlocfilehash: 0d3da94a76b36251d629f82b1575328c7ac10b26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="verify-a-vpn-gateway-connection"></a><span data-ttu-id="6ffb1-103">VPN Gateway 연결 확인</span><span class="sxs-lookup"><span data-stu-id="6ffb1-103">Verify a VPN Gateway connection</span></span>

<span data-ttu-id="6ffb1-104">이 문서에서는 어떻게 tooverify 클래식 hello와 리소스 관리자 배포 모델에 대 한 VPN 게이트웨이 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ffb1-104">This article shows you how tooverify a VPN gateway connection for both hello classic and Resource Manager deployment models.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="6ffb1-105">Azure portal</span><span class="sxs-lookup"><span data-stu-id="6ffb1-105">Azure portal</span></span>

[!INCLUDE [Azure portal](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <a name="powershell"></a><span data-ttu-id="6ffb1-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6ffb1-106">PowerShell</span></span>

<span data-ttu-id="6ffb1-107">hello 리소스 관리자 배포에 대 한 VPN 게이트웨이 연결 tooverify PowerShell을 사용 하 여 모델을 최신 버전의 hello hello 설치 [Azure 리소스 관리자 PowerShell cmdlet](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="6ffb1-107">tooverify a VPN gateway connection for hello Resource Manager deployment model using PowerShell, install hello latest version of hello [Azure Resource Manager PowerShell cmdlets](/powershell/azure/overview).</span></span>

[!INCLUDE [PowerShell](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="azure-cli"></a><span data-ttu-id="6ffb1-108">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="6ffb1-108">Azure CLI</span></span>

<span data-ttu-id="6ffb1-109">hello 리소스 관리자 배포에 대 한 VPN 게이트웨이 연결 tooverify Azure CLI를 사용 하 여 모델을 최신 버전의 hello hello 설치 [CLI 명령을](https://docs.microsoft.com/cli/azure/install-azure-cli) (2.0 이상)입니다.</span><span class="sxs-lookup"><span data-stu-id="6ffb1-109">tooverify a VPN gateway connection for hello Resource Manager deployment model using Azure CLI, install hello latest version of hello [CLI commands](https://docs.microsoft.com/cli/azure/install-azure-cli) (2.0 or later).</span></span>

[!INCLUDE [CLI](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]


## <a name="azure-portal-classic"></a><span data-ttu-id="6ffb1-110">Azure Portal(클래식)</span><span class="sxs-lookup"><span data-stu-id="6ffb1-110">Azure portal (classic)</span></span>

[!INCLUDE [Azure portal](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]

## <a name="powershell-classic"></a><span data-ttu-id="6ffb1-111">PowerShell(클래식)</span><span class="sxs-lookup"><span data-stu-id="6ffb1-111">PowerShell (classic)</span></span>

<span data-ttu-id="6ffb1-112">PowerShell을 사용 하는 hello 클래식 배포에 대 한 VPN 게이트웨이 연결 모델 tooverify hello hello Azure PowerShell cmdlet의 최신 버전을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ffb1-112">tooverify your VPN gateway connection for hello classic deployment model using PowerShell, install hello latest versions of hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="6ffb1-113">수 있는지 toodownload 및 설치 hello [서비스 관리](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0) 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="6ffb1-113">Be sure toodownload and install hello [Service Management](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0) module.</span></span> <span data-ttu-id="6ffb1-114">' Add-azureaccount ' toolog toohello 클래식 배포 모델에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ffb1-114">Use 'Add-AzureAccount' toolog in toohello classic deployment model.</span></span>

[!INCLUDE [Classic PowerShell](../../includes/vpn-gateway-verify-connection-ps-classic-include.md)]

## <a name="next-steps"></a><span data-ttu-id="6ffb1-115">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6ffb1-115">Next steps</span></span>

* <span data-ttu-id="6ffb1-116">가상 컴퓨터 tooyour 가상 네트워크를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ffb1-116">You can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="6ffb1-117">단계는 [가상 컴퓨터 만들기](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6ffb1-117">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>
