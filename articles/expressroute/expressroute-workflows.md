---
title: "ExpressRoute 회로 구성 하기 위한 aaaWorkflows | Microsoft Docs"
description: "이 페이지에서는 express 경로 회로 및 피어 링 구성 하기 위한 hello 워크플로 통해"
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: 55e0418c-e0bf-44a7-9aa1-720076df9297
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: cherylmc
ms.openlocfilehash: 8e1dfc137401e0d6d53608ae6c8de0085e182eba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-workflows-for-circuit-provisioning-and-circuit-states"></a>회로에 대한 Express 경로 워크플로 프로비전 및 회로 상태
이 페이지에서는 hello 서비스 프로 비전 하 고 상위 수준에서 라우팅 구성 워크플로 안내합니다.

![](./media/expressroute-workflows/expressroute-circuit-workflow.png)

hello 다음 그림과 해당 단계 hello 작업 표시는 express 경로 회로 프로 비전 된 최종 간 순서 toohave에 수행 해야 합니다. 

1. PowerShell tooconfigure ExpressRoute 회로 사용 합니다. Hello에 hello 지침에 따라 [만들 ExpressRoute 회로](expressroute-howto-circuit-classic.md) 을 참조 하십시오.
2. Hello 서비스 공급자에서 연결을 요청 합니다. 이 프로세스는 다양합니다. 방법에 대 한 자세한 내용은 연결 공급자에 게 문의 tooorder 연결 합니다.
3. hello 회로가 프로 비전 되어 성공적으로 프로 비전 상태 PowerShell 통해 hello ExpressRoute 회로 확인 하 여 확인 합니다. 
4. 라우팅 도메인을 구성합니다. 연결 공급자가 사용자를 위해 3계층을 관리하는 경우 회로에 라우팅을 구성합니다. 연결 공급자 계층 2 서비스 제공을 구성 해야 hello에 설명 된 지침 당 라우팅 [라우팅 요구 사항](expressroute-routing.md) 및 [라우팅 구성을](expressroute-howto-routing-classic.md) 페이지입니다.
   
   * Azure 개인 피어 링을 사용 하도록 설정-클라우드 내 가상 네트워크에 배포 된 서비스 / 피어 링이 tooconnect tooVMs를 사용 하도록 설정 해야 합니다.
   * Azure 공용 피어 링-공용 IP 주소에 호스팅된 tooconnect tooAzure 서비스 하려는 경우 Azure 공용 피어 링 설정 해야 합니다. Azure 개인 피어 링 용 tooenable 기본 라우팅 선택한 경우 요구 사항 tooaccess Azure 리소스입니다.
   * Microsoft 피어 링-사용이 tooaccess Office 365, Dynamics 365 사용 하도록 설정 해야 합니다. 
     
     > [!IMPORTANT]
     > 별도 프록시를 사용 하 여 / 가장자리 tooconnect tooMicrosoft hello에 사용할 하나 보다 hello 인터넷 확인 해야 합니다. ExpressRoute와 인터넷 hello에 대 한 동일한 가장자리 비대칭 라우팅 되며 네트워크에 대 한 연결 중단을 일으킬 hello를 사용 합니다.
     > 
     > 
     
     ![](./media/expressroute-workflows/routing-workflow.png)
5. 연결 가상 네트워크를 회로 tooExpressRoute-가상 네트워크 tooyour ExpressRoute 회로 연결할 수 있습니다. 지침에 따라 [toolink Vnet](expressroute-howto-linkvnet-arm.md) tooyour 회로 합니다. 이러한 Vnet 수 hello hello ExpressRoute 회로와 동일한 Azure 구독 또는 다른 구독에 있을 수 있습니다.

## <a name="expressroute-circuit-provisioning-states"></a>Express 경로 회로 상태 프로비전
각 Express 경로 회로에는 두 가지 상태가 있습니다.

* 서비스 공급자 프로비전 상태
* 가동 상태

상태는 Microsoft의 프로비전 상태를 나타냅니다. 이 속성은 tooEnabled Expressroute 회로 만들 때

hello 연결 공급자에 대 한 프로 비전 상태가 hello 연결 공급자 측 hello 상태를 나타냅니다. *프로비전되지 않음*, *프로비전 중* 또는 *프로비전됨*일 수 있습니다. hello ExpressRoute 회로에 있어야 하면 toobe 수 toouse에 대 한 프로 비전 됨 상태 것 합니다.

### <a name="possible-states-of-an-expressroute-circuit"></a>Express 경로 회로의 가능한 상태
이 섹션 아웃 ExpressRoute 회로 대 한 hello 가능한 상태를 나열합니다.

**만드는 경우**

Hello PowerShell cmdlet toocreate hello ExpressRoute 회로 실행 상태를 그 다음 hello에 hello ExpressRoute 회로 볼 수 있습니다.

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


**연결 공급자 hello 프로세스 hello 회로 프로 비전 된 경우**

ExpressRoute 회로 hello 상태를 그 다음에 hello hello 서비스 키 toohello 연결 공급자를 전달 합니다. 표시 되 고 hello를 프로 비전 프로세스 시작 합니다.

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled


**연결 공급자 hello를 프로 비전 프로세스가 완료 되 면**

나타납니다 hello ExpressRoute 회로 hello hello 연결 공급자 hello를 프로 비전 프로세스를 완료 하는 즉시 상태 뒤에 있습니다.

    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled

프로 비전 하 고 사용할 수는 hello 상태 hello 회로 가능에서 있습니다 toobe 수 toouse에 대 한 것입니다. 2계층 공급자를 사용하는 경우 이 상태인 경우 회로에 라우팅을 구성할 수 있습니다.

**연결 공급자 hello 회로가 프로 비전 해제 되는 경우**

Hello 서비스 공급자 toodeprovision hello ExpressRoute 회로 요청한 경우 hello 회로 서비스 공급자 hello hello 프로세스를 프로 비전 해제를 완료 된 후 상태를 다음 toohello 설정 표시 됩니다.

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


Toore 기능을 사용 하도록 선택할 수 필요에 따라 또는 toodelete hello 회로 PowerShell cmdlet을 실행 하는 경우.  

> [!IMPORTANT]
> 실행 하는 경우에 hello hello ServiceProviderProvisioningState는 프로 비전 또는 프로 비전 됨 hello 작업 하는 경우 PowerShell cmdlet toodelete hello 회로 실패 합니다. 먼저 연결 공급자 toodeprovision hello ExpressRoute 회로와 협력 하세요 하 고 hello 회로 삭제 합니다. Microsoft는 hello PowerShell cmdlet toodelete hello 회로 실행할 때까지 toobill hello 회로 계속 합니다.
> 
> 

## <a name="routing-session-configuration-state"></a>라우팅 세션 구성 상태
hello BGP 프로 비전 상태를 사용 하면 Microsoft edge hello에서 hello BGP 세션을 사용 하는지 여부를 알 수 있습니다. hello 상태를 설정 해야 하면 toobe 수 toouse hello 피어 링입니다.

Microsoft 피어 링에 대 한 특히 중요 한 toocheck hello BGP 세션 상태입니다. 또한 toohello BGP 프로 비전 상태에 라는 다른 상태 *공용 접두사 상태 보급*합니다. hello 공용 접두사 상태에 있어야 합니다. 보급 *구성* 모두 사용자 라우팅 toowork에 종단 간 및를 BGP 세션 toobe hello에 대 한 상태입니다. 

Hello 공용 접두사 상태는 tooa 설정 알린 경우 *필요한 유효성 검사* 상태 이면 hello BGP 세션을 설정 하지 않으면 hello 알리는 접두사 hello와 일치 하지 않습니다 hello 라우팅 레지스트리 중 하나에 숫자입니다. 

> [!IMPORTANT]
> Hello 상태 공용 접두사를 보급 하는 경우에 *수동 유효성 검사* 상태 이면 지원 티켓을 열어야 [Microsoft 지원](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) hello IP 주소를 따라 보급을 소유 하 고 있는 증거를 제공 하 고 hello로 익명 시스템 번호를 연결 합니다.
> 
> 

## <a name="next-steps"></a>다음 단계
* Express 경로 연결을 구성합니다.
  
  * [ExpressRoute 회로 만들기](expressroute-howto-circuit-arm.md)
  * [라우팅 구성](expressroute-howto-routing-arm.md)
  * [VNet tooan ExpressRoute 회로 연결](expressroute-howto-linkvnet-arm.md)

