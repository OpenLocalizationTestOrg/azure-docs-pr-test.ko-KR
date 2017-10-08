---
title: "ExpressRoute에 대 한 요구 사항 aaaQoS | Microsoft Docs"
description: "이 페이지는 Express 경로 회로에 QoS를 구성하고 관리하는 자세한 요구 사항을 제공합니다."
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: db1c1447-0283-4a09-907b-ae481adc40c7
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: cherylmc
ms.openlocfilehash: 46cc81bd38ff50dd9e7a1bfdd0faa457ff7b2fa1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-qos-requirements"></a>Express 경로 QoS 요구 사항
비즈니스용 Skype에는 차별화된 QoS 처리를 필요로 하는 다양한 워크로드가 있습니다. ExpressRoute 통해 tooconsume 음성 서비스 하려는 경우 아래에 설명 된 toohello 요구를 준수 해야 합니다.

![](./media/expressroute-qos/expressroute-qos.png)

> [!NOTE]
> QoS 요구 toohello Microsoft 피어 링만 적용 됩니다. hello Azure 공용 피어 링 및 Azure 개인 피어 링에 수신 하 여 네트워크 트래픽 DSCP 값 재설정 too0 됩니다. 
> 
> 

hello 다음 표에서 비즈니스용 Skype를 사용한 DSCP 표시의 목록. 너무 참조[비즈니스용 Skype에 대 한 QoS 관리](https://technet.microsoft.com/library/gg405409.aspx) 자세한 정보에 대 한 합니다.

| **트래픽 클래스** | **처리(DSCP 표시)** | **비즈니스 워크로드용 Skype** |
| --- | --- | --- |
| **음성** |EF (46) |Skype/Lync 음성 |
| **대화형** |AF41 (34) |비디오, VBSS |
| AF21 (18) |앱 공유 | |
| **기본값** |AF11 (10) |파일 전송 |
| CS0 (0) |다른 항목 | |

* Hello 워크 로드를 분류 하 고 hello 오른쪽 DSCP 값을 표시 해야 합니다. 제공 된 hello 지침에 따라 [여기](https://technet.microsoft.com/library/gg405409.aspx) 방법에 네트워크의 tooset DSCP 표시 합니다.
* 네트워크 내에서 여러 QoS 큐를 구성하고 지원해야 합니다. 음성 독립 실행형 클래스와 RFC 3246에 지정 된 hello EF 처리 합니다. 
* Hello 큐 메커니즘, 정체 검색 정책 및 트래픽 클래스 마다 대역폭 할당을 결정할 수 있습니다. 그러나 hello DSCP 비즈니스 작업에 대 한 Skype에 대 한 표시 유지 해야 합니다. 위에 나열 되지 않은 DSCP 표시를 사용 하는 경우 예를 들어 AF31 (26)를 다시 작성 해야이 DSCP 값 too0 hello 패킷 tooMicrosoft 보내기 전에 합니다. Microsoft는만 hello DSCP 값 테이블 위에 hello에 표시 된 것으로 표시 하는 패킷을 전송 합니다. 

## <a name="next-steps"></a>다음 단계
* Toohello 요구 사항에 대 한 참조 [라우팅](expressroute-routing.md) 및 [NAT](expressroute-nat.md)합니다.
* Hello 다음 링크 tooconfigure ExpressRoute 연결을 참조 하십시오.
  
  * [ExpressRoute 회로 만들기](expressroute-howto-circuit-classic.md)
  * [라우팅 구성](expressroute-howto-routing-classic.md)
  * [VNet tooan ExpressRoute 회로 연결](expressroute-howto-linkvnet-classic.md)

