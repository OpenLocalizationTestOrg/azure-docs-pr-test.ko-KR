---
title: "Azure 네트워크 감시자에서 aaaIntroduction toonext 홉 | Microsoft Docs"
description: "이 페이지에서는 다음 홉 기능 hello 네트워크 감시자의 개요를 제공"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: febf7bca-e0b7-41d5-838f-a5a40ebc5aac
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 916af736d0d52abadeafed746f0f8a0173b11033
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toonext-hop-in-azure-network-watcher"></a>Azure 네트워크 감시자에서 toonext 홉 소개

트래픽이 VM에서 NIC와 관련 된 hello 유효 경로에 따라 tooa 대상 전송 다음 홉에서 특정 가상 컴퓨터 및 NIC. hello 다음 홉 형식이 및 패킷의 IP 주소를 가져옵니다. 이렇게 하면 hello 패킷 되 toohello 방향이 지정 된 대상 또는 black 되 고 hello 트래픽 숨어 경우 toodetermine 있습니다. 여기서 트래픽이 방향이 지정 된 tooan 온-프레미스 위치 또는 가상 어플라이언스, hello 사용자별 경로의 됨으로써 구성이 tooconnectivity 문제가 발생할 수 있습니다. 또한 다음 홉 hello 다음 홉와 관련 된 hello 경로 테이블을 반환 합니다. 다음 홉을 hello 경로 사용자 정의 경로로 정의 된 경우 쿼리할 때 해당 경로 반환 됩니다. 그렇지 않은 경우 다음 홉은 "시스템 경로"를 반환합니다.

![다음 홉 개요][1]

hello 다음은 목록 다음 홉을 쿼리할 때 반환 될 수 있는 hello 다음 홉 형식입니다.

* 인터넷
* VirtualAppliance
* VirtualNetworkGateway
* VnetLocal
* HyperNetGateway
* VnetPeering
* 없음

### <a name="next-steps"></a>다음 단계

다음 홉 toofind toouse 네트워크 연결에 방문 하 여 발급 하는 방법에 대해 알아봅니다 [검사 hello 다음 홉 VM에서](network-watcher-check-next-hop-portal.md)

<!--Image references-->
[1]: ./media/network-watcher-next-hop-overview/figure1.png













