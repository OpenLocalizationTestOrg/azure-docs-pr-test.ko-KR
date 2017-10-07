---
title: "aaaEnabling 끝 tooend에서 Azure 응용 프로그램 게이트웨이 SSL | Microsoft Docs"
description: "이 페이지는 hello 응용 프로그램 게이트웨이 끝 tooend SSL 지원의 개요를 제공 합니다."
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: 3976399b-25ad-45eb-8eb3-fdb736a598c5
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: amsriva
ms.openlocfilehash: c5cb398a1e7d9a08662a3120baad98edb5575917
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-end-tooend-ssl-with-application-gateway"></a>응용 프로그램 게이트웨이 함께 SSL 종료 tooend 개요

응용 프로그램 게이트웨이 toohello 백 엔드 서버에 암호화 되지 않은 트래픽을 일반적으로 흐름 후 hello 게이트웨이에서 SSL 종료를 지원 합니다. 웹 서버 toobe unburdened 암호화 및 암호 해독 오버 헤드에서이 기능을 사용 합니다. 그러나 일부 고객에 대 한 암호화 되지 않은 통신 toohello 백 엔드 서버는 허용 가능한 옵션이 아닙니다. 이 암호화 되지 않은 통신 toosecurity 요구 사항, 규정 준수 요구 사항 원인일 수 있습니다 또는 hello 응용 프로그램에 보안 연결이 허용 될 수 있습니다. 이러한 응용 프로그램에 대 한 응용 프로그램 게이트웨이 지원 끝 tooend SSL 암호화 합니다.

## <a name="overview"></a>개요

최종 tooend SSL을 사용 하면 toosecurely 여전히 계층 7 부하 분산 기능의 hello 이점 활용 하기 위해 응용 프로그램 게이트웨이 제공 하는 동안 암호화 toohello 백 엔드 중요 한 데이터를 전송 합니다. 이러한 기능 중 일부는 쿠키 기반 세션 선호도, URL 기반 라우팅, 지원 사이트, 또는 기능 tooinject 전달-X 기반 라우팅에 대 한 * 헤더입니다.

최종 tooend SSL 통신 모드를 구성 하는 경우 응용 프로그램 게이트웨이 hello 게이트웨이에서 hello SSL 세션을 종료 하 고 사용자 트래픽을 해독 합니다. 규칙 tooselect hello 구성에 적절 한 백 엔드 풀 인스턴스 tooroute 트래픽을 다음 적용합니다. 그런 다음 응용 프로그램 게이트웨이 새 SSL 연결 toohello 백 엔드 서버를 시작 하 고 다시 hello 요청 toohello 백 엔드를 전송 하기 전에 hello 백 엔드 서버 공개 키 인증서를 사용 하 여 데이터를 암호화 합니다. 이 BackendHTTPSetting tooHTTPS에서 프로토콜 설정을 설정 하 여 SSL을 사용 하는 최종 tooend tooa 백 엔드 풀을 적용 합니다. 인증서 tooallow 보안 통신에 SSL을 사용 하는 최종 tooend hello 백 엔드 풀에서 각 백 엔드 서버 구성 되어야 합니다.

![최종 tooend ssl 시나리오][1]

이 예제에서는 TLS1.2를 사용 하 여 요청은 최종 tooend SSL을 사용 하 여 Pool1에 라우트된 toobackend 서버입니다.

## <a name="end-tooend-ssl-and-whitelisting-of-certificates"></a>최종 tooend SSL 및 인증서의 허용 목록

응용 프로그램 게이트웨이 백 엔드 알려진된도 hello 응용 프로그램 게이트웨이 통해 해당 인증서를 허용 목록에 있는 통신 합니다. 인증서의 허용 목록을 tooenable, 백 엔드 서버 인증서 toohello 응용 프로그램 게이트웨이 (hello 루트 인증서가 아닌)의 hello 공개 키를 업로드 해야 합니다. 만 연결 tooknown 및 허용 목록에 백 엔드 다음 허용 됩니다. 백 엔드 남은 hello 게이트웨이 오류가 발생 합니다. 자체 서명된 인증서는 테스트 용도이며 프로덕션 워크로드에는 권장하지 않습니다. 이러한 인증서가 hello를 사용 하려면 먼저 이전 단계에 설명 된 대로 hello 응용 프로그램 게이트웨이와 toobe 허용 목록.

## <a name="next-steps"></a>다음 단계

최종 tooend SSL에 대 한 학습 한 후 전환 너무[응용 프로그램 게이트웨이에 끝 tooend SSL을 사용 하도록 설정](application-gateway-end-to-end-ssl-powershell.md) 사용 하 여 응용 프로그램 게이트웨이 toocreate tooend SSL 종료 합니다.

<!--Image references-->

[1]: ./media/application-gateway-backend-ssl/scenario.png
