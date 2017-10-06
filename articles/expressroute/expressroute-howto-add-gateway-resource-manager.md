---
title: "ExpressRoute에 대 한 가상 네트워크 게이트웨이 tooa VNet 추가: PowerShell: Azure | Microsoft Docs"
description: "이 문서에서는 이미 ExpressRoute에 대 한 리소스 관리자 VNet을 만든 VNet 게이트웨이 tooan를 추가 하는 과정을 안내 합니다."
documentationcenter: na
services: expressroute
author: charwen
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 63e0bd60-abad-4963-8e27-3aa973e0d968
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/17/2017
ms.author: charwen
ms.openlocfilehash: 8983430b426ad7c4af766294fa16427c5e9df5c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-powershell"></a>PowerShell을 사용하여 ExpressRoute에 대한 가상 네트워크 게이트웨이 구성
> [!div class="op_single_selector"]
> * [Resource Manager - Azure Portal](expressroute-howto-add-gateway-portal-resource-manager.md)
> * [Resource Manager - PowerShell](expressroute-howto-add-gateway-resource-manager.md)
> * [클래식 - PowerShell](expressroute-howto-add-gateway-classic.md)
> * [비디오 - Azure Portal](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

이 문서 단계별로 hello 단계 tooadd, 크기 조정 및 기존 VNet에 대 한 가상 네트워크 (VNet) 게이트웨이 제거 합니다. 이 구성에 대 한 hello 단계 ExpressRoute 구성에 사용할 hello 리소스 관리자 배포 모델을 사용 하 여 만든 Vnet에 대 한 구체적으로 합니다. 가상 네트워크 게이트웨이 및 ExpressRoute의 게이트웨이 구성 설정에 대한 자세한 내용은 [ExpressRoute에 대한 가상 네트워크 게이트웨이 정보](expressroute-about-virtual-network-gateways.md)를 참조하세요. 


## <a name="before-beginning"></a>시작하기 전에
Hello 최신 Azure PowerShell cmdlet을 설치 했는지 확인 합니다. Toodo hello 최신 cmdlet를 설치 하지 않은 경우 해야 하므로 hello 구성 단계를 시작 하기 전에. 자세한 내용은 [Azure PowerShell 설치 및 구성](/powershell/azure/overview)을 참조하세요.

[!INCLUDE [expressroute-gateway-rm-ps](../../includes/expressroute-gateway-rm-ps-include.md)]

## <a name="next-steps"></a>다음 단계
Hello VNet 게이트웨이 만든 후에 VNet tooan ExpressRoute 회로 연결할 수 있습니다. 참조 [가상 네트워크 tooan ExpressRoute 회로 연결](expressroute-howto-linkvnet-arm.md)합니다.

