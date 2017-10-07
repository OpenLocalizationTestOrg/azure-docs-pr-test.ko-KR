---
title: "PowerShell을 사용하여 ExpressRoute용 VNet 게이트웨이 구성: classic: Azure | Microsoft Docs"
description: "Express 경로 구성을 위해 PowerShell을 사용하여 클래식 배포 모델 VNet에 대한 VNet 게이트웨이 구성"
documentationcenter: na
services: expressroute
author: charwen
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: 85ee0bc1-55be-4760-bfb4-34d9f2c96f30
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: charwen
ms.openlocfilehash: 6f37d4d9cba546b5416ab99040f5ef6dae273380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-powershell-classic"></a>PowerShell을 사용하여 ExpressRoute용 가상 네트워크 게이트웨이 구성(클래식)
> [!div class="op_single_selector"]
> * [Resource Manager - PowerShell](expressroute-howto-add-gateway-resource-manager.md)
> * [클래식 - PowerShell](expressroute-howto-add-gateway-classic.md)
> * [비디오 - Azure Portal](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

이 문서에서는 안내 hello 단계 tooadd 통해 크기 조정 및 기존 VNet에 대 한 가상 네트워크 (VNet) 게이트웨이 제거 합니다. hello이 구성에 대 한 단계는 hello를 사용 하 여 만든 Vnet에 맞게 **클래식 배포 모델** 될 및 ExpressRoute 구성에서 사용할 수 있습니다. 

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

**Azure 배포 모델 정보**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="before-beginning"></a>시작하기 전에
이 구성에 필요한 hello Azure PowerShell cmdlet을 설치 했는지 확인 하십시오 (1.0.2 이상의). Toodo hello cmdlet를 설치 하지 않은 경우 해야 하므로 hello 구성 단계를 시작 하기 전에. Azure PowerShell 설치에 대 한 자세한 내용은 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.

[!INCLUDE [expressroute-gateway-classic-ps](../../includes/expressroute-gateway-classic-ps-include.md)]

## <a name="next-steps"></a>다음 단계
Hello VNet 게이트웨이 만든 후에 VNet tooan ExpressRoute 회로 연결할 수 있습니다. 참조 [가상 네트워크 tooan ExpressRoute 회로 연결](expressroute-howto-linkvnet-classic.md)합니다.

