---
title: "회사 인터넷 도메인 tooa 트래픽 관리자 도메인 이름 aaaPoint | Microsoft Docs"
description: "이 문서는 회사 도메인 이름 tooa 트래픽 관리자 도메인 이름이 가리키도록 데 도움이 됩니다."
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 29822946-2d45-4434-ba47-fc180a445cc3
ms.service: traffic-manager
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/11/2016
ms.author: kumud
ms.openlocfilehash: 84c428f60a1dc70452bf957d98a68c95e0b51715
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="point-a-company-internet-domain-tooan-azure-traffic-manager-domain"></a>회사 인터넷 도메인 tooan Azure 트래픽 관리자 도메인 가리키기

Traffic Manager 프로필을 만들 때에는 Azure에서 해당 프로필에 DNS 이름을 자동으로 할당합니다. DNS 영역에서 이름을 toouse 트래픽 관리자 프로필의 toohello 도메인 이름을 매핑하는 CNAME을 DNS 레코드를 만듭니다. Hello 트래픽 관리자 도메인 이름은 hello에서 찾을 수 **일반** hello 트래픽 관리자 프로필의 hello 구성 페이지에서 섹션.

예를 들어 toopoint 이름 www.contoso.com toohello 트래픽 관리자 DNS 이름 contoso.trafficmanager.net 만들면 됩니다 DNS 리소스 레코드의 다음 hello:

    www.contoso.com IN CNAME contoso.trafficmanager.net

모든 트래픽이 너무 요청*www.contoso.com* 너무 웹 사이트로 이동*contoso.trafficmanager.net*합니다.

> [!IMPORTANT]
> 와 같은 두 번째 수준 도메인을 연결할 수 없습니다 *contoso.com*, toohello 트래픽 관리자 도메인입니다. DNS 프로토콜 표준에서는 두 번째 수준 도메인 이름에 대한 CNAME 레코드를 허용하지 않습니다.

## <a name="next-steps"></a>다음 단계

* [트래픽 관리자 라우팅 방법](traffic-manager-routing-methods.md)
* [트래픽 관리자 - 프로필 사용 안 함, 사용 또는 삭제](disable-enable-or-delete-a-profile.md)
* [트래픽 관리자 - 끝점 사용 안 함 또는 사용](disable-or-enable-an-endpoint.md)
