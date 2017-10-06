---
title: "다중 테 넌 트 백의 aaaOverview Azure 응용 프로그램 게이트웨이로 끝나는 | Microsoft Docs"
description: "이 페이지는 다중 테 넌 트 백 엔드에 대 한 hello 응용 프로그램 게이트웨이 지원의 개요를 제공합니다."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: 
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/26/2017
ms.author: gwallace
ms.openlocfilehash: b7da8c9c68e34bd83ad2b828fab62c00caea354a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="application-gateway-support-for-multi-tenant-back-ends"></a>Application Gateway는 다중 테넌트 백 엔드를 지원합니다.

Azure Application Gateway는 가상 컴퓨터 확장 집합, 네트워크 인터페이스, 공개/개인 IP 또는 FQDN(정규화된 도메인 이름)을 백 엔드 풀의 일부로 지원합니다. 기본적으로 응용 프로그램 게이트웨이 hello 클라이언트에서 들어오는 hello HTTP 호스트 헤더를 변경 되지 않습니다 및 보냅니다 hello 헤더 변경 되지 않은 toohello 백 엔드 합니다. 와 같은 많은 서비스에는 [Azure 웹 앱](../app-service-web/app-service-web-overview.md) 및 [API 관리](../api-management/api-management-key-concepts.md) 본질적으로 다중 테 넌 트 되 고 특정 호스트 헤더 또는 SNI 확장 tooresolve toohello 올바른 끝점을 사용 합니다. 이제 응용 프로그램 게이트웨이 헤더에 대 한 사용자가 toooverwrite hello 들어오는 HTTP 호스트 hello 백 엔드 HTTP 설정에 따라 hello 기능을 지원 합니다. 이 기능을 사용하면 다중 테넌트 백 엔드 Azure 웹앱 및 API 관리를 지원할 수 있습니다. 이 기능은 표준 hello 및 WAF SKU를 모두 사용할 수 있습니다. 다중 테 넌 트 백 지원을 작동 하는 SSL 종료 및 종료 tooend SSL 시나리오를 종료 합니다.

![웹앱 시나리오](./media/application-gateway-web-app-overview/scenario.png)

호스트 재정의에서 정의 된 hello 기능 toospecify hello HTTP 설정 및 수 수 적용된 tooany 다시 종료 풀 규칙을 만드는 중입니다. 다중 테 넌 트 다시 다음 호스트 헤더 및 SNI 확장 재정의의 두 가지 방법 지원 hello를 종료 합니다.

1. hello 기능 tooset hello 호스트 이름 tooa 고정 hello에는 값의 HTTP 설정 합니다. 이 기능은 hello 호스트 헤더를 재정의 하도록 해 줍니다 toothis hello HTTP 설정이 적용 될 모든 트래픽 toohello 백 엔드 풀에 대 한 값입니다. 최종 tooend SSL을 사용할 경우이 재정의 된 호스트 이름은 hello SNI 확장에에서 사용 됩니다. 이 기능을 사용 하면 시나리오 백 엔드 풀 팜 고객 호스트 헤더를 들어오는 hello와는 다른 호스트 헤더를 예상 하는 위치입니다.

2. hello 기능 tooderive hello 호스트 이름 IP hello 또는 hello 백 엔드 풀 멤버의 FQDN입니다. 또한 HTTP 설정은 개별 백 엔드 풀 멤버에서 hello 옵션 tooderive 호스트 이름으로 구성 하는 경우 백 엔드 풀 멤버의 FQDN에서 toopick hello 호스트 이름을 제공 합니다. 끝 tooend SSL을 사용할 경우이 호스트 이름은 FQDN hello에서 파생 되 고 hello SNI 확장에에서 사용 됩니다. 이 기능을 사용 하면 백 엔드 풀을 Azure 웹 앱과 유사한 두 개 이상의 다중 테 넌 트 PaaS 서비스를 가질 수 있습니다 hello 요청의 호스트 헤더 tooeach 멤버 FQDN에서 파생 된 hello 호스트 이름을 포함 하는 시나리오입니다.

> [!NOTE]
> 두 hello의 경우 앞에 있는 hello 설정을 hello 실시간 트래픽 동작과 상태 프로브 동작 하지 hello에만 적용 됩니다. 사용자 지정 프로브를 지원 hello 기능 toospecify hello 프로브 구성에 호스트 헤더가 이미 합니다. 사용자 지정 프로브 이제도 지원 hello 기능 tooderive hello 호스트 헤더에서에서 동작 hello 현재 구성 된 HTTP 설정 합니다. 이 구성은 hello를 사용 하 여 지정할 수 있습니다 `PickHostNameFromback endAddress` hello 프로브 구성에서 매개 변수가 있습니다. 최종 tooend 기능 toowork hello 프로브와 hello HTTP 설정을 모두에 수정 된 tooreflect hello에 대 한 올바른 구성 이어야 합니다.

이 기능을 통해 고객 hello 옵션 hello HTTP 설정 및 사용자 지정 프로브 toohello 적절 한 구성을 지정 합니다. 이 설정은 다음 연결 tooa 수신기와 다시 하는 규칙을 사용 하 여 풀을 종료 합니다.

## <a name="next-steps"></a>다음 단계

자세한 내용은 tooset 백업용으로 웹 앱과 응용 프로그램 게이트웨이를 방문 하 여 풀 멤버를 종료 하는 방법: [응용 프로그램 게이트웨이 사용 하 여 구성 앱 서비스 웹 앱](application-gateway-web-app-powershell.md)
