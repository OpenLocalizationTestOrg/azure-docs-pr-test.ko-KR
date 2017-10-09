---
title: "Azure 가상 네트워크에 영향을 주지는 Azure 서비스 중단의 hello 이벤트에서 aaaWhat toodo | Microsoft Docs"
description: "Azure 가상 네트워크에 영향을 주지는 Azure 서비스 중단의 hello 이벤트에서 어떤 toodo에 알아봅니다."
services: virtual-network
documentationcenter: 
author: NarayanAnnamalai
manager: jefco
editor: 
ms.assetid: ad260ab9-d873-43b3-8896-f9a1db9858a5
ms.service: virtual-network
ms.workload: virtual-network
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2016
ms.author: narayan;aglick
ms.openlocfilehash: db022d2a042d255cf8ec6afb68cd8436aeecfe08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-network--business-continuity"></a>가상 네트워크 – 비즈니스 연속성
## <a name="overview"></a>개요
가상 네트워크 (VNet)는 hello 클라우드에서 네트워크의 논리적 표현입니다. 사용자 고유의 개인 IP 주소 공간 및 세그먼트 hello 네트워크 서브넷으로 toodefine가 있습니다. Vnet은 Azure 가상 컴퓨터 및 클라우드 서비스 (웹/작업자 역할)와 같은 컴퓨팅 리소스 신뢰 경계 toohost로 사용 됩니다. VNet에 호스팅된 hello 리소스 간에 직접 개인 IP 통신할을 수 있습니다. 가상 네트워크 VPN 게이트웨이 또는 express 경로 같은 hello 하이브리드 옵션 중 하나를 통해 온-프레미스 네트워크를 연결 된 tooan 될 수도 있습니다.

VNet 지역 hello 범위 내에서 만들어집니다. 두 개의 서로 다른 지역에 같은 주소 공간으로 Vnet을 만들 수 있습니다 (예: 미국 동부 및 미국 서 부 있지만 이러한 tooone 연결할 수 없습니다 다른 직접). 

## <a name="business-continuity"></a>비즈니스 연속성
여러 가지 방법으로 응용 프로그램이 중단될 수 있습니다. 지정된 된 지역의 수 완전히 잘릴 수 기한 tooa 자연 재해 또는 여러 장치/서비스의 tooa 오류 인해 부분 재해. VNet 서비스가 hello에 미치는 영향을 hello 이러한 각각의이 상황에 차이가 있습니다.

**Q: tooan 전체 지역 가동 중단의 hello 이벤트에서 할까요? 즉, tooa 자연 재해 인해 완전히 구분 지역 인지 확인 하는 경우 Hello 지역에서 가상 네트워크가 호스트 toohello 어떻게 되나요?**

A: hello 가상 네트워크 및 hello 리소스 hello에 지역 남아를 hello 서비스 중단의 hello 시간 동안 액세스할 수 없는 영향을 받습니다.

![간단한 가상 네트워크 다이어그램](./media/virtual-network-disaster-recovery-guidance/vnet.png)

**Q: 수 있는 작업 toodo 다시 만드는 다른 지역에 있는 동일한 가상 네트워크를 hello?**

A: 가상 네트워크(VNet)는 비교적 경량의 리소스입니다. Azure Api toocreate VNet을 호출할 수 있습니다 hello로에 같은 주소 공간 다른 지역에 있습니다. toore-hello 만들기 hello에 존재 했던 동일한 환경에 지역 영향을 받는, toomake API 호출 toore 있는-클라우드 서비스 (웹/작업자 역할) 및 사용 된 가상 컴퓨터를 배포 합니다. 또한 toospin VPN 게이트웨이 및 온-프레미스 연결 (예: 하이브리드 배포)를 설치한 경우 tooyour 온-프레미스 네트워크에 연결 해야 합니다.

VNet을 만들기 위한 hello 지침은 있습니다 [여기](virtual-networks-create-vnet-arm-pportal.md)합니다. 

**Q: 지정된 지역의 VNet 복제본을 미리 다른 지역에 다시 만들 수 있나요?**

A: 예, hello를 사용 하 여 동일한 개인 IP 주소 공간 및 리소스 앞의 두 개의 서로 다른 지역에서 시간을 두 개의 Vnet을 만들 수 있습니다. 고객이 호스팅하는 경우가 인터넷 서비스 hello VNet에에서 연결은 활성화 된 트래픽 관리자 toogeo 경로 트래픽 toohello 영역을 설정할 수도 있습니다. 그러나 고객 두 Vnet를 연결할 수 없습니다 hello와 같은 주소 공간 tootheir 온-프레미스 네트워크 라우팅 문제를 발생 시키는 것입니다. 재해의 hello 시간 및 지역에서 VNet 손실, 고객 연결할 수 hello 일치 하는 주소 공간 tootheir 온-프레미스 네트워크와 함께 사용할 수 있는 지역에서 다른 VNet hello 합니다.

VNet을 만들기 위한 hello 지침은 있습니다 [여기](virtual-networks-create-vnet-arm-pportal.md)합니다.

